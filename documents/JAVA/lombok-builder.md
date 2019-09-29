# Lombok -Builder

Object를 생성할때 생성자에 데이터 값을 집어 넣을 경우를 생각해보자. 만약 생성자에 들어가는 변수가 바뀌거나 생성자에 넣어야 하는 변수의 순서가 바뀐다면 해당 생성자를 사용해 Object를 생성한 모든 소스를 수정해 주어야 한다. 이를 방지 하기 위하여 Lombok의 Builder 를 사용 할 수 있다.

### 1.Entity에 Builder 추가

아래와 같이 Entity 파일에 **@Builder** 를 추가해 준다.

```java 
package com.example.admin.model.entity;

import lombok.Builder;
import lombok.Data;
import lombok.ToString;
import lombok.experimental.Accessors;
import org.springframework.data.annotation.CreatedBy;
import org.springframework.data.annotation.CreatedDate;
import org.springframework.data.annotation.LastModifiedBy;
import org.springframework.data.annotation.LastModifiedDate;
import org.springframework.data.jpa.domain.support.AuditingEntityListener;

import javax.persistence.*;
import java.time.LocalDateTime;
import java.util.List;

@Entity
@Table(name="user")
@Data
@ToString(exclude = "orderGroupList")
@EntityListeners(AuditingEntityListener.class)
@Builder  //<< builder
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String account;
    private String password;
    private String status;
    private String email;
    private String phoneNumber;
    private LocalDateTime registeredAt;
    private LocalDateTime unregisteredAt;
    @CreatedDate
    private LocalDateTime createdAt;
    @CreatedBy
    private String createdBy;
    @LastModifiedDate
    private LocalDateTime updatedAt;
    @LastModifiedBy
    private String updatedBy;

    @OneToMany(fetch = FetchType.LAZY, mappedBy="user")
    private List<OrderGroup> orderGroupList;
}

```

### 2. Builder 사용

builder를 사용하여 아래와 같이 **builder()** 함수 이후, 생성자에 셋팅하고 싶은 값을 연결 한 후 마지막에 **build()** 를 해주면 해당 값을 가진 Object가 생성이 된다.

```java 
String account = "Test03";
String password = "Test03";
String status = "REGISTERED";
String email = "Test02@gmail.com";
String phoneNumber = "010-1234-3333";
LocalDateTime registeredAt = LocalDateTime.now();
        //builder
User user = User.builder().account(account).password(password)
            .status(status).email(email)
            .phoneNumber(phoneNumber).registeredAt(registeredAt).build();
```

### 3. Accessors(chain=true)  설정

builder와 비슷한 기능을 하는 **@Accessors(chain = true)** 을 Entity에 추가해 주자. 해당 기능은 함수를 연결 하여 사용할 수 있도록 도와준다.

```java 
@Entity
@Table(name="user")
@Data
@ToString(exclude = "orderGroupList")
@EntityListeners(AuditingEntityListener.class)
@Builder
@Accessors(chain = true) // < chain
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String account;
    private String password;
    private String status;
    private String email;
    private String phoneNumber;
    private LocalDateTime registeredAt;
    private LocalDateTime unregisteredAt;
    @CreatedDate
    private LocalDateTime createdAt;
    @CreatedBy
    private String createdBy;
    @LastModifiedDate
    private LocalDateTime updatedAt;
    @LastModifiedBy
    private String updatedBy;

    @OneToMany(fetch = FetchType.LAZY, mappedBy="user")
    private List<OrderGroup> orderGroupList;
}
```

### 4. Accessors(chain=true) 테스트

 **@Accessors(chain = true)**  을 통해 다음과 같이 여러 함수를 바로 연결 지어서 실행 시킬 수 있다.

```java 
user.setRegisteredAt(LocalDateTime.now()).setPassword("1234");
```

