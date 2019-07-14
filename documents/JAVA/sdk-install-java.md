# SDKMAN으로 JAVA 설치하기

### 1. SDKMAN이란 무엇일까?

Sdkman 이란 대부분 Unix 를 기반으로 한 시스템 내의 여러가지 Software Development Kits(SDK)의 버전들을 관리할 수 있도록 도와주는 도구이다. sdkman은 candidate(즉, 설치하고 싶은 SDK)들을 설치,제거, 변경, 목록 들을 쉽게 확인 할 수 있도록 편리한 CLI(Command Line Interface)를 제공해준다. 

> sdkman 으로 설치할 수 있는 SDK목록 확인하는 방법

```linux 
sdk list
```

다음과 같이 입력하면 설치할 수 있는 sdk 리스트들을 확인 할 수 있다.



### 2. SDKMAN으로 Java 설치하는 방법

> 1) 우선 java 의 버전 리스트들을 확인해보자

```linux 
sdk list java
```

다음과 같이 명령어를 입력하면 설치할 수 있는 Java 버전이 나오는 것을 확인 할 수 있다.



> 2) java 설치

그중 설치하고 싶은 버전의 Identifier를 확인한 후 다음과 같은 명령어를 입력한다.

```linux 
sdk install java 12.0.1.j9-adpt
```

이제 Java가 설치되었는지 확인하기 위해 다음과 같은 명령어를 입력해보자.

```linux 
java --version
```

다음과 같이 입력하면 현재 설치된 java의 버전을 확인 할 수 있다.

만약 다른버전을 설치하고 싶으면 어떻게 해야할까? 

> 3) 다른 버전 설치후 default 버전 변경하기

```linux 
sdk list java
sdk install java 8.0.212-zulu  
```

다음과 같이 버전 java 버전 8을 설치해보자. 이 후 java —version을 입력하면 현재 default 로 선택되어있는 버전은 여전히 12.0.1 버전인 것을 확인 할 수 있다. 이를 바꾸기 위해서는 다음과 같이 입력하면 된다.

```linux 
sdk default java 8.0.212-zulu  
```

이제 다시 java —version을 통해 확인하면 설치된 java의 default 버전이 8.0.212로 변경 된 것을 확인 할 수있다.

> 4) 설치된 폴더 확인하기

```linux 
cd ~ //home으로 이동
cd .sdkman/candidates/java/
ll
```

다음과 같이 해당 폴더의 목록을 확인하면 다음과 같이 설치된 java버전들을 확인 할 수 있다.

```linux
drwxr-xr-x   5 mia  staff  160  7 13 16:43 .
drwxr-xr-x   4 mia  staff  128  7 13 16:45 ..
drwxr-xr-x  11 mia  staff  352  4 19 05:34 12.0.1.j9-adpt
drwxr-xr-x  18 mia  staff  576  4 12 16:25 8.0.212-zulu
lrwxr-xr-x   1 mia  staff   49  7 13 16:43 current -> /Users/dh/.sdkman/candidates/java/12.0.1.j9-adpt/
```

위의 폴더 리스트를 확인해보면  current에 java 12.0.1.j9-adpt 버전이 링크로 지정되어 있는 것을 확인 할 수 있는데 해당 버전이 내컴퓨터에 설치된 java 버전들중 default값인 버전이다.





