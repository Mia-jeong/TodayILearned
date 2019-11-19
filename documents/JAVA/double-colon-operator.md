# Java 에서 :: (Double colon) 사용 방법

### 1. :: operator 란?

`::` method을 불르는 데 사용 된다. 형식은 아래와 같다.

`<Class name> :: <Method name>`

### 2. 예제

- Lamda expression

  - `stream.forEach(s-> System.out.println(s))`  > `stream.forEach(System.out::println(s))`

- Static Method : `className :: methodName`

  ```java 
  class Example {
    static void myFunc(String s){
      System.out.println(s);
    }
    
    public static void main (String[] args){
      List<String> list = new ArrayList<String>();
      list.add("hello");
      list.add("world");
      list.add("!");
      
      list.forEach(Example::myFunc);
      // return
      // hello
      // world
      // !
    }
  }
  ```

- Instance method : `objectOfClass :: methodName`

  ```java 
  class Example {
    void myFunc(String s){
      System.out.println(s);
    }
    
    public static void main (String[] args){
      List<String> list = new ArrayList<String>();
      list.add("hello");
      list.add("world");
      list.add("!");
      
      list.forEach((new Example())::myFunc);
      // return
      // hello
      // world
      // !
    }
  }
  ```

- Super method: `super :: someSuperClassMethod`

  ```java 
  class Parent {
    String print(String str){
      return ("Say Hi to " + str + "\n");
    }
  }
  
  class Children extends Parent {
    @Override
    String print(String s){
      Function<String, String> func = super::print;
      
      String newValue = func.apply(s);
      newValue += "Bye Bye " + s + "\n";
      
      return new newValue;
    }
    
    public static void main (String[] args){
      List<String> list = new ArrayList<String>();
      list.add("Mia");
      list.add("Bam");
      
      list.forEach(new Children()::print);
      //return 
      //Say Hi to Mia
      //Bye Bye Mia
      //Say Hi to Bam
      //Bye Bye Bam
    }
  }
  ```

- 특정한 Type의 Object의 Instance Method: `ClassName :: MethodName`

  ```java 
  class Greeting {
    String str = null;
    Greething(String str){
      this.str = str;
    }
    
    void hello(){
      System.out.println("Hello, "+this.str);
    }
  }
  
  class Example {
    public static void main(String[] args){
      List<String> list = new ArrayList<String>();
      list.add(new Greeting("Mia"));
      list.add(new Greeting("Bam"));
      
      list.forEach(Greeting::hello);
    }
  }
  ```

- Class Constructor : `ClassName :: new`

  ```java 
  class Example {
    public Example(String s){
      Systme.out.println("Example: " + s);
    }
    
    public static void main (String args[]){
      List<String> list = new ArrayList<String>();
      list.add(new Greeting("A"));
      list.add(new Greeting("B"));
      
      list.forEach(Example::new);
    }
  }
  ```


  