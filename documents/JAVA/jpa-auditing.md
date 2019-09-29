# JPA AUDITING

테이블을 생성하면 대부분 각각의 테이블마다 createdAt, createdBy, updatedAt, updatedBy 컬럼이 존재 할 것이다. 이걸 모든 테이블을 insert하거나 update할때마다 실행시키려고 하면 너무 지겨운 작업이 될 것이다. 그렇기 때문에 대신 **jpa auditing (감시 활성화)**를 사용 할 수 있다.



### 1. config 파일 생성

config package를 생성한 후 다음과 같이 JpaConfig 파일을 생성한다. 이 후, **@Configuration** 과 **@EnableJpaAuditing** 주석을 달아준다.

```java 
package com.example.admin.config;

import org.springframework.context.annotation.Configuration;
import org.springframework.data.jpa.repository.config.EnableJpaAuditing;

@Configuration
@EnableJpaAuditing //감시활성화
public class JpaConfig {

}
```

### 2. 감시를 실행할 파일 생성

Component package를 생성 후 다음과 같이 로그인 유저를 감시하는 파일을 생성하자. **@Component** 주석을 달아 준후 **AuditorAware<T>** 인터페이스를 implements시켜주자. 이후 **getCurrentAuditor()** 함수를 Override 한 후 Optional.of("로그인 유저") 의 아이디를 적어 return 해주자.

```java 
package com.example.admin.component;


import org.springframework.data.domain.AuditorAware;
import org.springframework.stereotype.Component;

import java.util.Optional;

//f로그인 유저 감시
@Component
public class LoginUserAuditorAware implements AuditorAware<String> {
    @Override
    public Optional<String> getCurrentAuditor() {
        return Optional.of("AdminServer");
    }
}

```

### 3. Entity 설정

이후, 감시 하에 있어야 하는 Entity 클래스에 **@EntityListeners(AuditingEntityListener.class)  ** 다음과 같은 주석을 추가해 준다.

그 다음 아래와 같이 각각의 주석(@) 과 변수들을 매핑 시켜준다.

- @CreatedDate : createdAt
- @CreatedBy : createdBy
- @LastModifiedDate : updatedAt
-  @LastModifiedBy: updatedBy

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
@EntityListeners(AuditingEntityListener.class)  // < auditor listening
@Builder
@Accessors(chain = true)
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



​	