# hashcode 

### 1. Hashcode

Hash Code란 Object를 식별할 수 있는 하나의 Integer값을 의마한다. Object의 hashCode() 함수는 Object의 메모리 번지를 사용하여 hashCode를 리턴하므로 Object마다 각각 다른 값을 가지고 있다. 객체의 값이 같은지 비교할 경우 Collection Framework 에서 HashMap, HashTable, HashSet은 다음과 같은 방법으로 두 객체가 같은지 비교한다.

- hashCode()를 실행시켜 return 된 해시코드 값이 같은지 확인
- 그 이후, equals method를 통해 두개의 Object가 같은지 비교.
- 위의 조건들이 모두 충족될때 서로 같은 객체로 판단

### 2. 사용 용도

다음과 같은 예제를 살펴보자.

```java 
List<String> words = Arrays.asList("computer", "keyboard", "laptop");
if (words.contains("keyboard")) {
    System.out.println("got it!");
}
```

위와 같이 특정 단어가  List에 속해있는지 확인하려면 선형시간 O(n) 이 걸릴 게 될 것이다. 이러한 점을 향상시키기 위하여 Java는 hash tables를 implementation한 Map이라는 자료구조를 사용한다. 

hash tables를 사용할때 **hashCode()** 라는 함수를 통해 주어진 key(ex. Keyboard)값의 hash value를 계산하며 이러한 hash value를 key값으로 데이터를 저장한다.



### 3.hashCode가 동작하는 방식

- hashCode는 단순하게 보자면 hashing algorithm을 통해 생성된 Integer (정수) 를 반환 한다.

- 두개의 Object가 서로 같다면 (equals) 해당 Object들의 hash value들은 동일한 값을 가질 것이다. 
- 그러나 Object가 다르다고 hash value가 반드시 다른건 아니다. 
- 하지만 Object가 서로 다를때 서로 다른 hash value값을 return 하는게 hash tables의 성능 문제를 향상 하는데 좋다.



### 4. bad hashCode

```java 
public class User {
 
    private long id;
    private String name;
    private String email;

    @Override
    public int hashCode() {
        return 1;
    }
         
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null) return false;
        if (this.getClass() != o.getClass()) return false;
        User user = (User) o;
        return id == user.id 
          && (name.equals(user.name) 
          && email.equals(user.email));
    }
}
```

위의 코드를 보자 User 클래스로 생성된 Object들은 모두 똑같은 Hash value를 갖게 될것이다. 이러한 hash value로 데이터를 저장한다면 모든 Object들은 똑같은 bucket에 저장이 된다. 

해당 bucket에 특정데이터가 포함되어있는지 확인해야 한다면 선형시간 O(n)의 시간이 걸려 hash tables를 사용 하는 의미가 없어질 것이다.

### 5. improved hashCode

```java 
@Override
public int hashCode() {
    return (int) id * name.hashCode() * email.hashCode();
}
```

다음과 같이 hashCode를 수정한다면 적어도 모든 Object가 hash value를 가지지 않을 테고 equals method가 바뀌지 않고 영속적이라면 꽤 합리적인 hashCode가 될 것이다.

### 6.Standard hashCode

```java 
@Override
public int hashCode() {
    int hash = 7;
    hash = 31 * hash + (int) id;
    hash = 31 * hash + (name == null ? 0 : name.hashCode());
    hash = 31 * hash + (email == null ? 0 : email.hashCode());
    return hash;
}
```

위의 hashcode는 일반적으로 사용되는 hashCode이다

```java 
@Override
public int hashCode() {
    final int prime = 31;
    int result = 1;
    result = prime * result + ((email == null) ? 0 : email.hashCode());
    result = prime * result + (int) (id ^ (id >>> 32));
    result = prime * result + ((name == null) ? 0 : name.hashCode());
    return result;
}
```

특히 Lombok이라는 library를 사용 한다면 위와 비슷하게 다음과 같은 hashCode를 자동으로 생성해주는 것을 확인할 수 있다(name과 email변수들은 해당 클래스에 속해있는 변수들로 각각 클래스마다 변경 됨)

위의 hashCode 함수들은 **31** 이란 값을 사용하는 것을 알 수 있는데 31을 사용하면 bitwise shift가 가능하여 그냥 곱하기를 계산하는 것보다 성능이 훨씬 좋기 때문이다.

```java 
31 * i == (i << 5) - i
```



*참고 자료 : [java hash](https://www.baeldung.com/java-hashcode)*

