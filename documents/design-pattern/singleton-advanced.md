<h1><a name="header-n64" class="md-header-anchor md-print-anchor" href="af://n64"> </a><span>Singleton - 2</span></h1>
<p><span> 해당 포스트는 Singleton - 1 편의 후속 편이다.</span></p>
<h3><a name="header-n66" class="md-header-anchor md-print-anchor" href="af://n66"> </a><span>5.  Lazy Singleton and Thread Safety</span></h3>
<p><span>singleton을 우리가 원할때만 생성하고 thread 에 안전한 singleton을 만들려면 어떻게 해야할까 ? 🤔</span></p>
<p><span>우선 lazy singleton을 생성해보자.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>Lazy Singleton</span></p>
</blockquote>
<pre><code class='language-java' lang='java'>public class LazySingleton {

    private static LazySingleton instance;

    private LazySingleton() {
        System.out.println(&quot;lazy singleton&quot;);
    }

    public static LazySingleton getInstance() {
        if(instance == null) {
            instance = new LazySingleton();
        }
        return instance;
    }

}
</code></pre>
<p><span>다음과 같이 return 되는 instance가 null인 경우에만 LazySingleton 객체를 생성해주고 아니면 기존에 생성된 instance를 return 해주면 Lazy singleton을 생성 할 수있다.</span></p>
<p><span>하지만 멀티 쓰레드를 통해 다중의 쓰레드가 getInstance를 동시에 접근하는 방법을 예방해야한다.</span></p>
<p><span>이때 우리는 synchronized 를 사용할 수 있다.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>Thread safety</span></p>
</blockquote>
<p><span>synchronized 사용 방법에는 다음과 같이 두가지 방법이 있다.</span></p>
<p>&nbsp;</p>
<p><span>1) 동기화 하고 싶은 method에 synchronized keyword 추가 시켜주기.</span></p>
<pre><code class='language-java' lang='java'>public static synchronized LazySingleton getInstance() {
        if(instance == null) {
            instance = new LazySingleton();
        }
        return instance;
}
</code></pre>
<p>&nbsp;</p>
<p><span>2) synchronized  method를 통해 체크해주기.</span></p>
<pre><code class='language-java' lang='java'>public static LazySingleton getInstance(){
    if(instance == null){
        synchronized (LazySingleton.class){
            if (instance == null){
                instance = new LazySingleton();
            }
        }
    }
    return instance;
}
</code></pre>
<p>&nbsp;</p>
<p><span>이와 같이 synchronized를 추가해주면 다중 쓰레드가 동시접근 하는 것을 막을 수 있다.</span></p>
<p>&nbsp;</p>
<h3><a name="header-n89" class="md-header-anchor md-print-anchor" href="af://n89"> </a><span>6. Initialization-on-demand-holder - Inner Static Singleton</span></h3>
<p><span>동시접근을 막는 방법은 synchronized외에 다른 방법도 있다 바로 Singleton안에 새로운 클래스를 선언해주고 해당 클래스 결과를 리턴해주는 것이다.</span></p>
<p>&nbsp;</p>
<pre><code class='language-java' lang='java'>class InitOnDemandHolder{
    private InitOnDemandHolder(){}

    private static class Holder{
        private static final InitOnDemandHolder INSTANCE = new InitOnDemandHolder();
    }

    public static InitOnDemandHolder getInstance(){
        return Holder.INSTANCE;
    }
}
</code></pre>
<p>&nbsp;</p>
<p><span>이러한 방법을 Initialization-on-demand-holder idiom 이라고 부른다. 즉, java에서 클래스 안의 클래스 즉, 중첩 클래스(Impl)은 getInstance() 가실행되기 전까지는  참조 되지 않는다.그렇기 때문에 LazySingleton 기능을 수행 한다. 또한 Holder에 선언된 INSTANCE가 static으로 선언 되어있기 때문에 클래스 로딩 시점에 한 번만 호출되고 final을 써서 다시 값이 할당 되지 않는다. 그렇기 때문에 thread-safety역시 충족 시킨다. 현재로서는 가장 많이 사용되고 있는 싱글톤 패턴이다.</span></p>
<p>&nbsp;</p>
<h3><a name="header-n96" class="md-header-anchor md-print-anchor" href="af://n96"> </a><span>7. Enum Singleton</span></h3>
<p><span>singleton을 class 가 아님 Enum형태로 선언 할 수도 있다.</span></p>
<pre><code class='language-java' lang='java'>enum EnumBasedSingleton{
    INSTANCE;

    //it&#39;s always private
    EnumBasedSingleton(){
        value = 42;
    }

    private  int value;

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }
}
</code></pre>
<p><span>Enum의 생성자는 언제나 private으로 선언되어 인스턴스가 여러개 생기지 않도록 보장해준다. 또한 직렬화나 리플렉션 상황에서도 직렬화가 자동으로 지원되는 이점이 있다. 하지만 inherit을 사용 할 수 없으며 serialization을 효과적으로 할 수 없는 단점이 있다.</span></p>
<p><span>(참고 문서)</span></p>
<blockquote><p><span>1.12 Serialization of Enum Constants</span></p>
<p><span>Enum constants are serialized differently than ordinary serializable or externalizable objects. The serialized form of an enum constant consists solely of its name; field values of the constant are not present in the form. To serialize an enum constant, ObjectOutputStream writes the value returned by the enum constant&#39;s name method. To deserialize an enum constant, ObjectInputStream reads the constant name from the stream; the deserialized constant is then obtained by calling the java.lang.Enum.valueOf method, passing the constant&#39;s enum type along with the received constant name as arguments. Like other serializable or externalizable objects, enum constants can function as the targets of back references appearing subsequently in the serialization stream.</span></p>
<p><span>The process by which enum constants are serialized cannot be customized: any class-specific writeObject, readObject, readObjectNoData, writeReplace, and readResolve methods defined by enum types are ignored during serialization and deserialization. Similarly, any serialPersistentFields or serialVersionUID field declarations are also ignored--all enum types have a fixed serialVersionUID of 0L. Documenting serializable fields and data for enum types is unnecessary, since there is no variation in the type of data sent.</span></p>
</blockquote>
<p>&nbsp;</p>
<pre><code class='language-java' lang='java'>public class EnumSingleton {
    static void saveToFile(EnumBasedSingleton singleton, String fileName) throws  Exception
    {
        try(FileOutputStream fileOut = new FileOutputStream(fileName);
            ObjectOutputStream out = new ObjectOutputStream(fileOut)
        ){
            out.writeObject(singleton);
        }
    }

    static EnumBasedSingleton readFromFile(String fileName) throws Exception{
        try(FileInputStream fileIn = new FileInputStream(fileName);
            ObjectInputStream in = new ObjectInputStream(fileIn)){
            return (EnumBasedSingleton) in.readObject();
        }
    }

    public static void main(String[] args) throws Exception {
        String filename = &quot;myfile.bin&quot;;
        EnumBasedSingleton s1 = EnumBasedSingleton.INSTANCE;
        s1.setValue(111);
        saveToFile(s1, filename);

        EnumBasedSingleton s2 = readFromFile(filename);
        System.out.println(s2.getValue());
        System.out.println(s1 == s2);


    }
}
</code></pre>
<p><span>위의 예제를 살펴보자 다음 main method를 실행시키면 우리는 111을 얻게 될것이다. 하지만 해당 부분을 주석처리를 해버리면 어떻게 될까?</span></p>
<pre><code class='language-java' lang='java'>    public static void main(String[] args) throws Exception {
        String filename = &quot;myfile.bin&quot;;
        //EnumBasedSingleton s1 = EnumBasedSingleton.INSTANCE;
        //s1.setValue(111);
        //saveToFile(s1, filename);

        EnumBasedSingleton s2 = readFromFile(filename);
        System.out.println(s2.getValue());
        System.out.println(s1 == s2);


    }
</code></pre>
<p><span>우리는 42라는 값을 얻게 될것이다. 왜냐하면 Enum은 serialize을 할 당시 name 값만 저장하고 value값은 저장하지 않기 때문이다 따라서 deserialize를 할 경우 해당 Enum singleton의 valueOf method를 사용하여 저장된 name이 일치하는 값을 가져오기 때문에 42를 출력한다.</span></p>
<p>&nbsp;</p>
<h3><a name="header-n111" class="md-header-anchor md-print-anchor" href="af://n111"> </a><span>7. Monostate</span></h3>
<p><span>다음과 같이 변수들을 static으로 선언 하고 각각의 getter, setter method를 다음과 같이 작성하면 해당 클래스를 Single storage(Singleton)으로 사용할 수 있다.</span></p>
<pre><code class='language-java' lang='java'>public class Monostate {
    private static String name;
    private static int age;

    public String getName() {
        return Monostate.name;
    }

    public void setName(String name) {
        Monostate.name = name;
    }

    public int getAge() {
        return Monostate.age;
    }

    public void setAge(int age) {
        Monostate.age = age;
    }

    @Override
    public String toString() {
        return &quot;Monostate{&quot; +
                &quot;name=&#39;&quot; + Monostate.name + &#39;\&#39;&#39; +
                &quot;, age=&quot; + Monostate.age +
                &#39;}&#39;;
    }
}
</code></pre>
<p><span>이를 증명하기 위해 해당 클래스를 실행 시켜 보았다.</span></p>
<pre><code class='language-java' lang='java'>class Demo{
    public static void main(String[] args) {
        Monostate mono = new Monostate();
        mono.setName(&quot;Bam&quot;);
        mono.setAge(20);

        Monostate mono2 = new Monostate();
        System.out.println(mono2);
    }
}
</code></pre>
<p><return>
<span>Monostate{name=&#39;Bam&#39;, age=20}</span></p>
<p><span>다음과 같이 mono2의 값은 mono에서 세팅해준 값과 동일 하다. 왜냐하면 해당 클래스는 이제 singleton으로 작동 하기 때문디ㅏ.</span></p>
<p>&nbsp;</p>
<h3><a name="header-n119" class="md-header-anchor md-print-anchor" href="af://n119"> </a><span>8. Multition</span></h3>
<p><span>여러종류의 객체를 담고 있는 singleton을 만드려면 어떻게 해야 할까? 다음과 같이 생성하면 된다.</span></p>
<pre><code class='language-java' lang='java'>// 1. enum
enum Subsystem{
    AMERICANO,
    CAFELATTE,
    CAFFUCCINO
}

class CoffeeMachine{
    private static int instanceCount = 0;
    private CoffeeMachine(){
        instanceCount++;
        System.out.println(&quot;A total  of &quot;+instanceCount+&quot; instances created so far&quot;);
    }

  	// 2. 클래스를 담을 변수
    private static HashMap&lt;Subsystem, CoffeeMachine&gt; instances = new HashMap&lt;&gt;();

    // 3. 클래스를 생성 및 불러오는 함수
    public static CoffeeMachine get(Subsystem subsystem){
        if (instances.containsKey(subsystem)) return instances.get(subsystem);

        CoffeeMachine instance = new CoffeeMachine();
        instances.put(subsystem, instance);
        return instance;
    }
}
</code></pre>
<p><span>1) 먼저 enum으로 싱글톤으로 생성하고 싶은 객체의 종류를 정의하자.</span></p>
<p><span>2) 이 후, HashMap을 생성해 해당 클래스들을 담는 변수를 성하자.</span></p>
<p><span>3) 마지막으로 static method로 클래스를 불러 오는 함수를 생성하자. 미리 선언해둔 HashMap(instatnces) 에 해당 클래스의 인스턴스가 포함되어있으면 이미생성된 것을 불러오고 아니면 새로 생성하여 instances변수에 저장 할 것이다.</span></p>
<pre><code class='language-java' lang='java'>public class Multition {
    public static void main(String[] args) {
        CoffeeMachine main = CoffeeMachine.get(Subsystem.AMERICANO);
        CoffeeMachine aux = CoffeeMachine.get(Subsystem.CAFELATTE);
        CoffeeMachine fall = CoffeeMachine.get(Subsystem.CAFFUCCINO);
    }
}
</code></pre>
<p>&nbsp;</p>
