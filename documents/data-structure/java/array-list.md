# DataStructure - ArrayList

*다음 글은 Think Data Structures 자바로 배우는 핵심 자료구조와 알고리즘 을 읽고 정리한 글 입니다.*

JCF(Java Collection Framework) 한 종류인 ArrayList를 살펴보자.

### 1. ArrayList Class

다음과 같이 List 인터페이스를 상속받는 ArrayList 클래스가 존재한다. 앞으로 해당 클래스에 속해 있는 함수들과 해당 함수들의 BigO를 같이 계산해 보자.

```Java 
public class ArrayList<T> implements List<T> {
	int size;                    
	private T[] array;          

	@SuppressWarnings("unchecked")
	public ArrayList() {
		array = (T[]) new Object[10];
		size = 0;
	}
```



### 2. add()

해당 리스트에 변수를 추가하고 싶다면 add() 함수를 사용해야 한다. add()함수의 로직은 다음과 같다.

```Java 
	@Override
	public boolean add(T element) {
		if (size >= array.length) {
			@SuppressWarnings("unchecked")
			T[] bigger = (T[]) new Object[array.length * 2];
			System.arraycopy(array, 0, bigger, 0, array.length);
			array = bigger;
		}
		array[size] = element;
		size++;
		return true;
	}

```

먼저 우리가 add() 함수를 불러온다면 위의 함수가 실행 될 것이다. 함수 내부를 살펴보면 새로 변수를 추가할때 기존에 리스트가 가지고 있던 사이즈보다 크다면 **System.arraycopy()** 를 통해서 배열 사이즈가 2배인 array에 기존 array를 카피하여 사이즈를 크게 만든다. 

이때 걸리는 시간은 분활상환분석(평소 필요 + 최악의 경우 / n ) O(1)이다.

*분활상환 분석 : 최악의경우, 즉 배열을 copy하는 경우는 가끔 발생하지만 한 번 발생하면  그 후로는 오래동안 나타나지 않으므로 비용을 분활상환 

이후, copy가 끝나면 해당함수는 또 다른 add(int index, T element) 함수를 부른다.

```Java 
	@Override
	public void add(int index, T element) {
		if (index < 0 || index > size) {
			throw new IndexOutOfBoundsException();
		}
		add(element);
		for (int i=size-1; i>index; i--) {
			array[i] = array[i-1];
		}
		array[index] = element;
	}
```

위의 함수는 index 이 후의 숫자들을 뒤로 한칸씩 땡겨야 하므로 최악의 경우 O(n)이 걸린다. 따라서 add() 함수는 총 O(n)이 걸린다.

### 3. get()

```Java 
	@Override
	public T get(int index) {
		if (index < 0 || index >= size) {
			throw new IndexOutOfBoundsException();
		}
		return array[index];
	}
```

get() 함수는 위에서 보는바와 같이 O(1) 상수시간을 가진다.

### 4.set()

```java 
	@Override
	public T set(int index, T element) {
		// no need to check index; get will do it for us
		T old = get(index);
		array[index] = element;
		return old;
	}
```

set()함수 내부를 살펴보면 get()함수를 부른다. get()은 O(1) 상수시간을 가진다. 그 이후의 로직은 특정 index에 element를 단순 대입해주는 것이므로 set() 은 O(1) 상수시간을 가진다.



### 5. remove()

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
```

remove() 함수를 살펴보면 제일 먼저 indexOf() 함수를 부른다. indexOf() 함수는 다음과 같다.

```Java 
	@Override
	public int indexOf(Object target) {
		for (int i = 0; i<size; i++) {
			if (equals(target, array[i])) {
				return i;
			}
		}
		return -1;
	}
	private boolean equals(Object target, Object element) {
		if (target == null) {
			return element == null;
		} else {
			return target.equals(element);
		}
	}
```

indexOf 함수는 target을 발견할때까지 array를 순회하므로 O(n)의 시간이 걸린다. 이후 remove() 함수는 int 를 인자로 받는 또 다른 remove() 함수를 부른다.

```Java 
	@Override
	public T remove(int index) {
		T element = get(index);
		for (int i=index; i<size-1; i++) {
			array[i] = array[i+1];
		}
		size--;
		return element;
	}

```

해당 함수의 내부로직을 살펴보면  먼저, get() 은 O(1) 의 시간을 갖는다. 이 후, 지우려는 index부터 시작해서 data가 들어있는 길이까지 loop를 돌면서 index의 data들을 앞으로 한 칸씩 땡긴다. 이때 시간은 O(n)이 걸리므로 해당 함수는 O(n)이 걸린다.

위의 로직을 정리하면 remove 함수의 총 시간은 O(n)이 걸린다.