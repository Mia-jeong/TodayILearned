# Java Input/Output Stream(입출력 스트림) - 표준 입출력

### 1. Input/Output Stream?

- 네트 워크 에서 자료의 흐름이 물과 같다는 의미에서 유래 되었다.
- 다양한 입출력 장치에서 독립적으로 일관성 있는 입출력 방식ㅇ르 제공 한다.
- 입출력이 구현 되는 곳에서는 모두 I/O 스트림을 사용한다(키보드, 파일 디스크, 메모리 등)

### 2. I/O 구분

- I/O 대상 기준 

  - 입력 스트림 : 대상으로 부터 자료를 읽어 들임
    - FileInputStream, FileReader, BufferedInputStream, BufferedReader 등
    - `자바 응용 프로그램` ---<-----`입력스트림`---------`입출력자료`
  - 출력 스트림 :  대상으로 부터 자료를 출력
    - FileOutputStream, FileWriter, BufferedOutputStream, BufferedWriter등
    - `자바 응용 프로그램` --->-----`출력스트림`---------`입출력자료`

- 자료의 종류

  - 바이트 스트림: 바이트 단위로 자료를 읽고 쓴다
    - FileInputStream, FileOutputSteam, BufferedInputStream,BufferedOutputStream 등  
  - 문자 단위 스트림: 문자는 2바이트씩 처리 해야 한다.
    - FileReader, FileWriter, BufferedReader, BufferedWriter등

- 스트림의 기능

  - 기반 스트림: 대상에 자료를 읽고 쓰는 기능의 스트림
    - FileInputStream, FileOutputStream, FileReader, FileWriter 등
  - 보조 스트림: 직접 읽고 쓰는 기능은 없고 추가적인 기능을 제공해 주는 스트림, 기반 스트림이나 또 다른 보조스트림을 생성자의 매개변수로 포함(Decorator)
    - InputStreamReader, OutputSreamWriter, BufferedInputStream, BufferedOutputStream등

  

  

### 3. 표준 입출력 - System

`System` 클래스의 표준 입출력 멤버

```java 
public class System{
  public static PrintStream out; //표준 출력 스트림
  public static InputStream in; //표준 입력 스트림
  public static PrintStream arr; //표준 에러 스트림
}
```

`Problem`

```java 
public class SystemInTest {

    public static void main(String[] args) throws IOException {
        System.out.println("입력 후 끝 이라고 쓰세요");
        int n ;
        while( (n = System.in.read())!= '끝'){
            System.out.print((char)n);
        }
    }
}
```

위와 같이 소스를 구현하면 `끝` 은 문자이기 때문에 2byte씩 구현 되어 제대로 작동 되지 않을 것이다.  `System.in.read()` 는 한 번에 1byte 밖에 읽지 못하기 때문이다. 그렇기 때문에 아래와 같이 InputStreamReader를 사용해주어야 한다. 

`InputStreamReader` 는 byte를 읽어 문자로 변환해주는 역할을 한다.

```java 
    public static void main(String[] args) throws IOException {
        System.out.println("입력 후 끝 이라고 쓰세요");
        int n ;
        InputStreamReader isr = new InputStreamReader(System.in);
        while( (n = isr.read())!= '끝'){
            System.out.print((char)n);
        }
    }
```

### 4. 표준 입출력 -Scanner 

- Java.util 패키지에 있는 입력 클래스
- 문자 뿐 아니라 정수, 실수 등 다양한 자료형을 읽을 수 있다.
- 생성자가 다양하여 여러 소스로 부터 자료를 읽을 수 있다.
  - Scanner(File Source) : 파일을 매개 변수로 받아 Scanner를 생성
  - Scanner(InputStream source): 바이트 스트림을 매개 변수로 받아 Scanner를 생성
  - Scanner(String source): String을 매개변수로 받아 Scanner를 생성

### 5. 표준 입출력 - Console 

- System.in 을 사용하지 않고 콘솔에서 표준 입출력이 가능
- Console 클래스의 method
  - String readLine() : 문자열을 읽는다.
  - char[] readPassword() : 사용자에게 문자열을 보여주지 않고 읽는다.
  - Reader reader() : Reader클래스를 반환
  - PrintWriter writer(): PrintWriter 클래스를 반환

```java 
public class ConsoleTest {

    public static void main(String[] args) {
        Console console = System.console();
        System.out.println("이름: ");
        String name = console.readLine();
        System.out.println("비밀번호: ");
        char[] password = console.readPassword();

        System.out.println("name " + name);
        System.out.println("password " + password);
    }
}
```



