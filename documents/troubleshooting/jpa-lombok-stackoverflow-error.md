# JPA에서 entity사용시 Lombok 으로 생성한 toString 으로 인해 StackOverFlow error발생시 해결방법



### 🔒 사건

Lombok을 사용하여 작성한 각각의 entity클래스에 서로 연결되어 있는 클래스끼리 @OneToMany , @ManyToMany로 연결 시켜 준후 테스트 코드를 작성 하였다.

**( Entity 1: User )**

```java 
@Entity
@Table(name="user")
@Data
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name="account")
    private String account;
    private String email;
    private String phoneNumber;
    private LocalDateTime createdAt;
    private String createdBy;
    private LocalDateTime updatedAt;
    private String updatedBy;

    @OneToMany(fetch = FetchType.LAZY, mappedBy = "user")
    private List<OrderDetail> orderDetailList;
}

```

User 클래스는 OrderDetail클래스와 1 : N형식으로 연결 되어 다음과 같이 @OneToMany annotation을 통해 entity를 연결 시켜주었다.

**( Entity 2: OrderDetail )**

```java 
@Entity
@Data
@AllArgsConstructor
@NoArgsConstructor
public class OrderDetail {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private LocalDateTime orderAt;

    @ManyToOne
    private User user;

    private Long itemId;
}
```

OrderDetail역시 User클래스와 N : 1 로 연결되어 있어 다음과 같이 @ManyToOne을 통해 entity를 연결 시켜주었다.

**( Test code )**

```java 
@Test
@Transactional
public void read(){
   Optional<User> selectedUser = userRepository.findById(6L);

   selectedUser.ifPresent(user -> {
      System.out.println("user: " + user);
      System.out.println("email: " + user.getEmail());
      user.getOrderDetailList().stream().forEach(detail ->{
          System.out.println("detail : " + detail.getId());
      });
   });
}
```

이후, 다음과 같이 User클래스와 OrderDetail클래스를 조인한 결과를 가져오는 테스트 코드를 작성하였다.

당연히 테스트가 통과할 것이라는 내 예상과는 달리 **StackOverFlow** 에러가 출력 되었다 😨
에러 내용은 다음과 같다.

```xml 
java.lang.StackOverflowError
	at java.base/java.lang.AbstractStringBuilder.append(AbstractStringBuilder.java:774)
	at java.base/java.lang.StringBuilder.append(StringBuilder.java:248)
	at java.base/java.time.LocalDate.toString(LocalDate.java:2180)
	at java.base/java.time.LocalDateTime.toString(LocalDateTime.java:1972)
	at java.base/java.lang.String.valueOf(String.java:2951)
	at java.base/java.lang.StringBuilder.append(StringBuilder.java:168)
	at com.example.admin.model.entity.OrderDetail.toString(OrderDetail.java:12)
	at java.base/java.lang.String.valueOf(String.java:2951)
	at java.base/java.lang.StringBuilder.append(StringBuilder.java:168)
	at java.base/java.util.AbstractCollection.toString(AbstractCollection.java:473)
	at org.hibernate.collection.internal.PersistentBag.toString(PersistentBag.java:601)
	at java.base/java.lang.String.valueOf(String.java:2951)
	at java.base/java.lang.StringBuilder.append(StringBuilder.java:168)
	at com.example.admin.model.entity.User.toString(User.java:12)
	at java.base/java.lang.String.valueOf(String.java:2951)
(..생략)
```

위의 에러를 자세히 보면 String과  관련 해서 에러가 나는 것을 알 수 있었다.

###  🔍 원인 

원인을 찾기 위해서 우선 Object 형태의 객체가 System.out.println()안에서 어떻게 작동하는지 먼저 파악해야 했다. 

그러기 위해서 다음과 같은 코드를 살펴보았다. 다음은 Java내장 함수인 println 의 소스이다.

```Java 
    public void println(Object x) {
        String s = String.valueOf(x);
        synchronized(this) {
            this.print(s);
            this.newLine();
        }
    }
```

다음과 같이 Object x가 들어오면 println 함수는 **String.valueOf()** 라는 함수를 통해 Object를 String으로 변환시켜서 출력 시킨다.
그렇다면 String.valueOf()는 어떻게 동작하는 것일까? 또 함수를 파고 들어가보자.

```Java 
    public static String valueOf(Object obj) {
        return obj == null ? "null" : obj.toString();
    }
```

다음과 같이 valueOf함수는 들어온 obj에 포함되어있는 toString() 함수를 불러와 return시키는 역할 을 한다.

즉, System.out.println()안에 Object를 넣으면 해당 Object의 **toString()** 함수를 불러오는 것이다. 그럼 이제 Lombok에서 자동으로 생성해준 toString() 함수를 살펴보자.

**( User )**

```Java 
public String toString() {
        return "User(id=" + this.getId() + ", account=" + this.getAccount() + ", email=" + 		
          this.getEmail() + ", phoneNumber=" + this.getPhoneNumber() + ", createdAt=" + 
          this.getCreatedAt() + ", createdBy=" + this.getCreatedBy() + ", updatedAt=" + 
          this.getUpdatedAt() + ", updatedBy=" + this.getUpdatedBy() + ", orderDetailList=" + 
          this.getOrderDetailList() + ")";
}
```

**( OrderDetail )**

```Java 
public String toString() {
        return "OrderDetail(id=" + this.getId() + ", orderAt=" + this.getOrderAt() + ", user=" 
          + this.getUser() + ", itemId=" + this.getItemId() + ")";
}
```

위와 같이 User 와 OrderDetail클래스 내부에는 **this.getOrderDetailList()** 와 **this.getUser()** 가 포함되어 있다. 이 두개의 Object가 계속해서 서로를 불러오기 때문에 무한루프에 빠져 결국 **StackOverFlow** 에러가 나는 것이다.

### 🔑 해결책

위와 같은 무한루프를 피하기 위해 **@ToString** 을 사용 하였다.

따라서 User 클래스와 OrderDetail클래스 상단에 다음과 같이 각각 추가해 주었다.

**( User )**

```Java 
@Entity
@Table(name="user")
@Data
@ToString(exclude = "orderDetailList")
public class User {
		//생략
}
```

**(OrderDetail)**

```Java 
@Entity
@Data
@AllArgsConstructor
@NoArgsConstructor
@ToString(exclude = "user")
public class OrderDetail {
	//생략
}
```

위와 같이 작성하여 각각 클래스의 toString함수에서 서로 연결되어있는 Object들을 제거 해주었다.

이후, 테스트를 다시 돌리니 에러 없이 원하는 결과 값이 도출 되었다.🎉







