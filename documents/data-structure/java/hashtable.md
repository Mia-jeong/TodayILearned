# DataStructure - HashTables



### 1. Hash Table

Hash table은 내부적으로 배열을 사용하여 데이터를 저장하기 때문에 빠른 검색속도를 갖는다. 특정 값을 접근하는데 해당 데이터의 고유한 index로 접근 하여 O(1)의 시간이 걸리는 것이 장점이다. 따라서 다음과 같이

```java 
List<String> words = Arrays.asList("computer", "keyboard", "laptop");
if (words.contains("keyboard")) {
    System.out.println("got it!");
}
```

리스트를 사용하여 데이터를 검색하면 O(n)의 시간이 걸리지만 Hash Table을 사용하면 O(1)의 시간이 걸릴 수 있다. 

(하지만 생성되는 Hashcode로직에 의해 항상 O(1)의 시간이 걸리는 것은 아님. )

### 2. Hash Table이 동작하는 방법

Hash Table에 데이터를 저장 하기 위해서는 먼저 해당 객체의 key값을 hashCode로 변환시킨다 이 후, 해당 hashCode를 배열의 index로 변경하여 해당 index에 데이터를 저장한다.

하지만 데이터를 저장하다보면 다른 객체가 똑같은 hashCode를 같게 되어 결국 똑같은 index에 저장되는 **Collision** 이 일어날 수 있다. 이러한 Collision이 많아질 수록 검색 시간은 O(1)에서 O(n)으로 시간이 늘어나게 된다.

### 3. Hash Table의 충돌을 피하는 방법

- **Open Addressing** : 데이터를 삽입하려는 해시 버킷이 이미 사용중인 경우 다른 해시 버킷에 해당 데이터를 삽입
- **Separate Chaining**: 각 배열의 인자를 링크드 리스트로 선언, 인덱스가 같은 Object는 동일한 해시 버킷의 리스트에 차곡차곡 저장한다.

둘 다 O(n)의 시간이 걸린다. 하지만 Open Addresing은 연속된 공간에 데이터를 저장하여 Separate Chaining에 비하면 캐시 효율이 높다. 따라서 데이터 개수가 충분히 적다면 Open Addresing 이 Separate Chaining 보다 성능이 우수하다. Java 7과 8모두 HashMap을 구현할때 Separate Chaining 방식으로 구현되었지만 Java8같은 경우 특정 배열의 범위를 초과하면 링크드리스트를 트리로 구조로 변환시켜 성능을 향상 시켰다.

참고 

1. [Java HashMap은 어떻게 동작하는가?](https://d2.naver.com/helloworld/831311)
2. [Data Structures: Hash Tables](https://www.youtube.com/watch?v=shs0KM3wKv8)

