# Lombok

### 1. Lombok이란 무엇일까?

Java 를 사용하여 개발하다보면 무수히 많은 Model(DTO or Bean)등을 생성할 것이다. 해당 클래스내의 변수들을 사용하기 위해 우리는 무수히 많은 getter, setter method를 생성한다. 물론 이클립스, IntelliJ와 같은 개발 툴들로 인하여 자동으로 생성 할 수 있지만 이러한 것 조차 매우 귀찮은 일이다. 그렇기 때문에 Lombok 이 탄생하였다. Lombok을 사용하여 하나의 annotaion을 class에 추가함으로써 우리는 더이상 해당 클래스의 getter, setter method를 생성할 필요가 없다 바로 lombok이 자동으로 생성해 주기 때문이다.

### 2. 사용방법

Spring Boot와 IntelliJ를 사용한다고 가정하여 사용방법을 작성해 보겠다.

1) IntelliJ의 Plugin에 Lombok을 검색하여 설치

2) build.gradle파일에 다음과 같이 Lombok dependency추가

```xml 
dependencies {
    compile('org.projectlombok:lombok')
}
```

3)Spring Boot 실행시 함수를 발견할 수 없다고 나온다면 Preferences > Build,Execution, Deployment> Compiler > Annotation Processors  창으로 이동하여 Enable annotation processing 체크 후 Apply 및 OK 클릭

### 3. 사용 예시

```java 
package com.example.study.model;


import lombok.AllArgsConstructor;
import lombok.Data;

@Data
@AllArgsConstructor
public class SearchParam {

    private String account;
    private String email;
    private int page;

}

```

*더 많은 Lombok 사용 예제와 annotation을 알고 싶다면 다음 사이트를 방문해보자.
[Lombok](https://projectlombok.org/features/all)