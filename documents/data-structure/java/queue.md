# Data Sturcture -Queue

- Queue는 상태가 서로 의존관계가 없을때 사용 된다, 즉 A와 B가 서로 관련이 없지만 모두 하긴 해야할때 Queue를 사용한다
- FIFO(First In First Out)의 구조를 가지고 있다.
- Scheduling에 주로 사용된다.
- BFS(Breadth First Search )에 주로 사용된다.
- 미로에서 최단 거리를 구할때 주로 사용 된다.

### 1. Queue 구조

```java 
public class Queue<T> {

    class Node<T> {
        private T data;
        private Node<T> next;

        public Node(T data) {
            this.data = data;
        }
    }

    private Node<T> first;
    private Node<T> last;

    public void add(T item){
        Node<T> temp = new Node<T>(item);
        if(last != null){
            last.next = temp;
        }
        last = temp;
        if(first == null){
            first = last;
        }
    }
    public T remove(){
        if(first == null) throw new NoSuchElementException();

        T temp = first.data;
        first = first.next;

        if(first == null) last = null;

        return temp;
    }

    public T peek(){
        if(first == null) throw new NoSuchElementException();
        return first.data;
    }

    public boolean isEmpty(){
        return first == null;
    }

}
```

Queue 에는 다음과 같이 add, remove, peek, isEmpty 의 4가지 함수가 존재한다.

### 2. Add

```java 
    public void add(T item){
        Node<T> temp = new Node<T>(item);
        if(last != null){
            last.next = temp;
        }
        last = temp;
        if(first == null){
            first = last;
        }
    }
```

- add함수는 Queue의 끝에 데이터를 집어 넣는 함수이다.
- add 함수는 다음과 같이 last 가 null이 아니라면 기존에 존재하던 last.next에 item으로 생성된 node(temp)를 참조 시켜준다. 이후, last에 해당 node를 다시 넣어준다.
- 이때 first가 null이라면 first에 last를 대입 시켜주어야 한다.

### 3. Remove

```java 
    public T remove(){
        if(first == null) throw new NoSuchElementException();

        T temp = first.data;
        first = first.next;

        if(first == null) last = null;

        return temp;
    }
```

- remove는 첫번째에 존재하는 데이터를 삭제 시켜주는 함수이다.
- 먼저 first가 null이면 exception을 발생 시켜준다.
- first가 존재 하다면 return시킬 데이터를 임시 저장(temp) 한 후 first 에 first.next값을 대입시킨다. 이때 만약 first가 null이 된다면 last도 null로 대입시켜주자.

### 4.Peek

```java 
    public T peek(){
        if(first == null) throw new NoSuchElementException();
        return first.data;
    }
```

- peek은 first에 있는 데이터를 반환 시켜주는 함수이다.
- 다음과 같이 first가 존재하지 않다면 exception을 던지고, 존재한다면 first의 data를 반환 시켜준다.

### 5.isEmpty

```java 
    public boolean isEmpty(){
        return first == null;
    }
```

- isEmpty는 Queue가 비어있는지 확인 시켜주는 함수이다.
- first가 null인지 체크하여 boolean으로 반환 시켜준다.