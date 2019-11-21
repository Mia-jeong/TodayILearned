# Java I/O Stream - 바이트 단위 입출력 스트림

### 1. 바이트 단위 입출력 스트림

- InputStream : 바이트 단위 입력 스트림 최상위 클래스

- OutputStream: 바이트 단위 출력 스트림 최상위 클래스

- 추상 메서드를 포함한 추상클래스로 하위 클래스가 구현하여 사용

- 주요 하위 클래스

  | Stream Class          | Description                                                  |
  | --------------------- | ------------------------------------------------------------ |
  | FileInputSteam        | 파일에서 바이트 단위로 자료를 읽는다.                        |
  | ByteArrayInputStream  | Byte 배열 메모리에서 바이트 단위로 자료를 읽는다.            |
  | FilterInputStream     | 기반 스트림에서 자료를 읽을 때 추가 기능을 제공하는 보조 스트림의 상위 클래스 |
  | FileOutputSream       | 바이트 단위로 파일에 자료를 쓴다.                            |
  | ByteArrayOutputStream | Byte 배열에 바이트 단위로 자료를 쓴다.                       |
  | FilterOutputStream    | 기반 스트림에서 자료를 쓸 때 추가 기능을 제공 하는 보조 스트림의 상위 클래스 |

  

### 2. FileInputStream & FileOutputStream

- 파일에 한 바이트씩 자료를 읽고 쓰는데 사용(문자는 못 읽음, 문자를 읽고 쓰고 싶으면 FileReader, FileWriter를 사용 해야함 )
- 입력 스트림은 파일이 없는 경우 예외 발생
- 출력 스트림은 파일이 없는 경우 파일 생성하여 출력

#### 1) FileInputStream 예제

**file 내용을 한 글자씩 읽는 방법**

```java 
    public static void main(String[] args) {
        try( FileInputStream fls = new FileInputStream("input.txt");) {
            int i;
            while( (i = fls.read()) != -1){
                System.out.println((char)i);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        System.out.println("end");
    }
```

**file 내용을 Array로 읽는 방법**

```java 
    public static void main(String[] args) {
        try( FileInputStream fls = new FileInputStream("input.txt");) {
            int i;
            byte[] bs = new byte[100];
            while( (i = fls.read(bs)) != -1){
              /*
                for (byte b : bs){
                    System.out.print((char)b);

                }*/
                //위와 같이 읽으면 사용되지 않는 배열 공간은 garbage 처리 되므로 
                //아래와 같이 읽어진 글자 길이 만큼 출력
                for (int j = 0; j < i ; j++) {
                    System.out.print((char)bs[j]);
                }
                System.out.println();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        System.out.println("end");
    }
```

#### 2)FileOutputStream 예제

```java 
    public static void main(String[] args) {

        byte[] bs = new byte[26];
        byte data = 65;
        for (int i = 0; i < bs.length; i++) {
            bs[i] = data++;
        }
        try(FileOutputStream fos = new FileOutputStream("alpha.txt", true);
            FileInputStream fls = new FileInputStream("alpha.txt")){
            /* 한줄 씩 작성
            fos.write(65);
            fos.write(66);
            fos.write(67);*/
            //Array로 작성
            fos.write(bs);
            int ch;
            while((ch = fls.read())!= -1){
                System.out.print((char)ch);
            }
        }catch (IOException e){
            e.fillInStackTrace();
        }
    }
```

