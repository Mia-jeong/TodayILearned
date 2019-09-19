# DataStructure - LinkedList

*다음 글은 Think Data Structures 자바로 배우는 핵심 자료구조와 알고리즘 을 읽고 정리한 글 입니다.*

JCF(Java Collection Framework) 한 종류인 LinkedList를 살펴보자.

### 1. LinkedList Class

다음과 같이 List 인터페이스를 상속받는 LinkedList 클래스가 존재한다. 앞으로 해당 클래스에 속해 있는 함수들과 해당 함수들의 BigO를 같이 계산해 보자. 해당클래스 안에는 다음과 같이 Node 클래스가 존재하며 Node 클래스는 서로의 데이터 주소를 참조하면서 연관관계를 이어 나갈 것이다.

```java 
public class LinkedList<E> implements List<E> {
  
	private class Node {
		public E cargo;
		public Node next;

		public Node(E cargo) {
			this.cargo = cargo;
			this.next = null;
		}
		public Node(E cargo, Node next) {
			this.cargo = cargo;
			this.next = next;
		}
		public String toString() {
			return "Node(" + cargo.toString() + ")";
		}
	}

	private int size;            
	private Node head;         

	public LinkedList() {
		head = null;
		size = 0;
	}
}
```

### 2. add()

```Java 
	@Override
	public boolean add(E element) {
		if (head == null) {
			head = new Node(element);
		} else {
			Node node = head;
			for ( ; node.next != null; node = node.next) {}
			node.next = new Node(element);
		}
		size++;
		return true;
	}
```

위의 함수를 살펴보자 다음 함수는 연결고리의 맨 끝에 새로운 Node를 추가시키는 함수이다. 만약 head가 null이라면 head에 새로운 Node 객체를 생성 하면 되지만 그렇지 않다면 head부터 끝까지 순회를 통해 마지막에 새로운 Node 객체를 추가해 주어야 한다. 따라서 해당 함수는 O(n)의 시간을 가진다.

```Java 
	@Override
	public void add(int index, E element) {
		// no need to check bounds; getNode does it.
		if (index == 0) {
			head = new Node(element, head);
		} else {
			Node node = getNode(index-1);
			node.next = new Node(element, node.next);
		}
		size++;
	}
```

위의 함수는 특정 index에 element를 추가 시켜주는 함수이다. 위의 함수를 살펴보면 해당 index에 add를 하기위해서 index바로 이전(index-1) 노드를 가져오기 위해 **getNode** 함수를 부른다. 

```java 
	private Node getNode(int index) {
		if (index < 0 || index >= size) {
			throw new IndexOutOfBoundsException();
		}
		Node node = head;
		for (int i=0; i<index; i++) {
			node = node.next;
		}
		return node;
	}
```

getNode() 함수는 다음과 같이 index까지 반복문문을 돌려 해당 Node를 찾아내는 형식이다 따라서 O(n)의 시간을 갖는다.



getNode()함수 이후 add()함수에서는 찾은 Node에 다음과 같이 **node.next = new Node(element, node.next)** 노드를 연결 시켜주면서 로직이 끝이 난다 따라서 add(int index, E element) 는 O(n)의 시간이 걸린다.

### 3. indexOf()

```java 
	@Override
	public int indexOf(Object target) {
		Node node = head;
		for (int i=0; i<size; i++) {
			if (equals(target, node.cargo)) {
				return i;
			}
			node = node.next;
		}
		return -1;
	}
```

특정 Data의 index를 찾아주는 indexOf() 함수는 다음과 같이 List의 Size만큼 반복문을 돌려 해당 data와 일치하는 데이터를 찾는다. 운이 좋으면 head데이터와 일치하겠지만 만약 해당 데이터가 size-1 에 있는 데이터와 일치한다면 size길이만큼 반복문이 돌아갈 것이다. 그렇기 때문에 해당 함수는 O(n)의 시간이 걸린다.

### 4. remove()

```java 
	@Override
	public boolean remove(Object obj) {
		int index = indexOf(obj);
		if (index == -1) {
			return false;
		}
		remove(index);
		return true;
	}

	@Override
	public E remove(int index) {
		E element = get(index);
		if (index == 0) {
			head = head.next;
		} else {
			Node node = getNode(index-1);
			node.next = node.next.next;
		}
		size--;
		return element;
	}
```

remove 함수를 살펴 보자 remove 함수내부를 보면 getNode()함수를 부른다 앞서 말했듯이 getNode()함수는 O(n)의 시간이 걸린다 이후, 반환된 node 의 next를 node.next.next로 대입시켜준다. 

따라서 remove()함수역시 O(n)의 시간이 걸린다



### 5. 참고 

Java에는 Garbage Collector가 존재한다. Garbage Collector는 쓰지 않는 메모리를 자동적으로 삭제 시켜주는 역할을 한다. 그러나 ArrayList인 경우 즉, 배열을 쓰는경우 그 리스트 자체가 파괴되지 않는 이상 Garbage Collector가 동작하지 않는다. 하지만 LinkedList일 경우 삭제를 통해 참조되지 않는 Node들은 Garbage Collector 에 의해 파괴 된다. 하지만 파괴되는 과정에서 삭제 되어야 하는 Node를 모드 파괴하는동안 O(n)의 시간이 들기때문에 성능문제가 오기도 한다.



### 6. ArrayList와 LinkedList , Doubly LinkedList 비교 

*Doubly LinkedList 란 list의 head뿐만 아니라 tail도 저장하는 리스트를 의미 한다.

| Category            | ArrayList | LinkedList | Doubly LinkedList |
| ------------------- | --------- | ---------- | ----------------- |
| add(끝)             | 1         | n          | 1                 |
| add(시작)           | n         | 1          | 1                 |
| add(일반적)         | n         | n          | n                 |
| get/set             | 1         | n          | n                 |
| indexOf/lastIndexOf | n         | n          | n                 |
| isEmpty/size        | 1         | 1          | 1                 |
| remove(끝)          | 1         | n          | 1                 |
| remove(시작)        | n         | 1          | 1                 |
| remove(일반적)      | n         | n          | n                 |

- Get/set 을 많이 사용 한다면 ArrayList 사용
- 시작과 끝에 add/remove를 많이 한다면 LinkedList(Doubly LinkedList) 사용
- 작은 문제에서는 딱히 중요하지 않다.
- ArrayList의 Data들은 배열의 한 덩어리 안의 메모리 안에 나란히 저장 되어 낭비되는 공간이 거의 없지만 LinkedList인 경우 하나 또는 두개의 참조 가 있는 노드가 필요하며 참조는 공간을 차지 한다. 그렇기 때문에 ArrayList보다 하드웨어 효율이 떨어질 수 있다.