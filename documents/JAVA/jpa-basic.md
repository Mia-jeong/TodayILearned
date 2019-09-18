# JPA Basic

### 1. JPA란 ?

- ORM( Object Relational Mapping)의 한 종류로 관계형 데이터 베이스(RDBMS)의 정보를 객체지향으로 손 쉽게 활용 할 수 있도록 도와주는 도구.
- Object(자바 객체) 와 Relation(관계형 데이터 베이스) 간 의 Mapping을 통해서 보다 손쉽게 적용할 수 있는 기술을 제공해준다.
- 쿼리에 집중 하기 보다 객체에 집중 함 으로써, 좀 더 프로그래밍 적으로 활용이 가능

### 2.Entity 란?

- **Entity**: 테이블을 자동으로 생성해주는 기능이 존재, 즉 DB Table == JPA Entity로 보면 된다.

- Annotation 종류

  | Annotation      | Description                                                  |
  | --------------- | ------------------------------------------------------------ |
  | @Entity         | 해당 Class가 Entity임을 명시                                 |
  | @Table          | - 실제 DB테이블 이름을 명시<br />- 클래스이름이 실제테이블이름과 같다면 굳이 명시하지 않아도 된다. |
  | @Id             | Index Primary Key를 명시                                     |
  | @Column         | 실제 DB Column 이름 명시                                     |
  | @GeneratedValue | Primary Key식별키의 전략 설정                                |

- JPA에서는 **snake case** 와 **camel case** 를 자동으로 매칭 시켜 준다.

(코드 예시)

```java 
package com.example.study.model.entity;

import lombok.Data;

import javax.persistence.*;
import java.time.LocalDateTime;

@Data
@Entity
@Table(name="user")
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
}

```



### 3. Repository

쿼리문을 작성하지 않아도 기본적인 CRUD(CREATE, READ, UPDATE, DELETE)를 자동으로 생성해준다.

### 4. JPA 연관관계 설정

| Relation | Annotation  |
| -------- | ----------- |
| 1 : 1    | @OneToOne   |
| 1 : M    | @OneToMany  |
| M : 1    | @ManyToOne  |
| M : M    | @ManyToMany |

### 5. Fetch 종료

| Fetch | Description                                                  |
| ----- | ------------------------------------------------------------ |
| LAZY  | - 지연 로딩<br />- SELECT * FROM TABLE WHERE id = ?<br />- 연관 관계에 있는 데이터에 대해 getMethod들을 쓰지않는 이상 해당 데이터를 로딩하지 않음<br />- OneToMany와 ManyToOne일 경우 사용하는 것이 좋음 |
| EAGER | - 즉시 로딩<br />- JOIN<br />- 한 번에 연관 관계에 있는 모든 데이터를 즉시 다 로딩함<br />- 성능의 저하가 올 수 있음<br />- 1 : 1의 경우에만 사용하는 것이 좋음 |

### 6. JPA 사용방법 

- gradle에 다음과 같이 설정 추가 (build.gradle)

  ```xml 
  dependencies {
      compile('org.springframework.boot:spring-boot-starter-data-jpa')
      compile('mysql:mysql-connector-java')
  }
  ```

- application.properties 파일에 다음과 같이 DB connection 정보 추가

  ```xml 
  #db source url
  spring.datasource.url=jdbc:mysql://localhost:3306/study?useSSL=false&useUnicode=true&serverTimezone=Asia/Seoul
  
  #db response name
  spring.datasource.username=root
  
  #db response password
  spring.datasource.password=pwd
  ```

- Entity class 생성

  ```Java  
  @Entity
  @Table(name="user")
  @Data
  @ToString(exclude = "orderDetailList")
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
  
      //user connected variable user of OrderDetail
      @OneToMany(fetch = FetchType.LAZY, mappedBy = "user") 
      private List<OrderDetail> orderDetailList;
  }
  ```

- Repository 생성 

  ```java 
  @Repository
  public interface UserRepository extends JpaRepository<User, Long> { //Long = dataType of PK 
  
      // select * from user where account = ? << test03
      Optional<User> findByAccount(String account);
  
      Optional<User> findByEmail(String email);
  
  }
  ```

- Test 

  ```java  
  public class UserRepositoryTest extends AdminApplicationTests {
  
  
      @Autowired //(DI = Dependency Injection)
      private UserRepository userRepository;
  
      @Test
      public void create(){
          User user = new User();
          user.setAccount("abc3@gmail.com");
          user.setCreatedAt(LocalDateTime.now());
          user.setCreatedBy("admin");
          user.setEmail("abc3@gmail.com");
          user.setPhoneNumber("010-1234-1234");
  
          User createdUser = userRepository.save(user);
          System.out.println("createdUser Id : " + createdUser.getId());
      }
  
      @Test
      @Transactional
      public void read(){
          //Optional<User> selectedUser = userRepository.findById(6L);
          Optional<User> selectedUser = userRepository.findByAccount("abc@gmail.com");
  
          selectedUser.ifPresent(user -> {
              System.out.println("user: " + user);
              System.out.println("email: " + user.getEmail());
          });
      }
  
      @Test
      public void update(){
  
          Optional<User> selectedUser = userRepository.findById(4L);
  
          selectedUser.ifPresent(user -> {
              user.setAccount("haha@gmail.com");
              user.setUpdatedAt(LocalDateTime.now());
              user.setUpdatedBy("admin");
              userRepository.save(user);
          });
  
      }
  
      @Test
      @Transactional //it would be rollback after test is done
      public void delete(){
          Optional<User> selectedUser = userRepository.findById(5L);
  
          Assert.assertTrue(selectedUser.isPresent());
  
          selectedUser.ifPresent(user -> {
              userRepository.delete(user);
          });
  
          Optional<User> deletedUser = userRepository.findById(5L);
  
          Assert.assertFalse(deletedUser.isPresent());
      }
  
  }
  ```

  