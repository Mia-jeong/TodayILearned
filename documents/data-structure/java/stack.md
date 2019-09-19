# DataStructure - Stack

- Stack은 주로 상태 즉, 발자취를 기억하는 용도로 많이 쓰인다.A라는 일을 마치기 위해 B라는 일을 먼저 끝내야 할때 사용된다.
- DFS(Depth First Search)에 주로 사용된다.
- LIFO(Last In First Out) 구조를 가지고 있어 마지막에 입력된 것이 제일 먼저 출력 되는 구조를 가지고 있다.
- Code를 실행 시킬때 우리는 **call stack** 구조를 통해 코드를 실행 시킨다.

### 1. Stack 구조

```Java 
public class Stack<T> {
    class Node<T> {
        private T data;
        private Node<T> next;

        public Node(T data) {
            this.data = data;
        }
    }
    private Node<T> top;

    public T pop(){
        if(top == null) throw new NoSuchElementException();
        T temp = top.data;
        top = top.next;
        return temp;
    }

    public void push(T data){
        Node temp = new Node<T>(data);
        temp.next=top;
        top = temp;
    }

    public T peek(){
        if(top == null) throw new NoSuchElementException();
        return top.data;
    }

    public boolean isEmpty(){
        return top == null;
    }

}

```

Stack에는 다음과 같이 push(), pop(), peek(), isEmpty(), size() 형태의 함수를 가진다.

### 2. Push

```java 
    public void push(T data){
        Node temp = new Node<T>(data);
        temp.next=top;
        top = temp;
    }
```

- push는 stack에 데이터를 집어 넣는 함수이다.

### 3. Pop

```Java 
    public T pop(){
        if(top == null) throw new NoSuchElementException();
        T temp = top.data;
        top = top.next;
        return temp;
    }
```

- pop은 stack의 최상단에 있는 값을 삭제 시키는 함수이다.

  

### 4.Peek

```Java 
    public T peek(){
        if(top == null) throw new NoSuchElementException();
        return top.data;
    }
```

- peek은 stack의 최상단 값을 불러 오는 함수이다.

  

### 5.isEmpty

```java 
    public boolean isEmpty(){
        return top == null;
    }
```

- isEmpty는 stack이 비어있는지 확인 하는 함수이다.

  