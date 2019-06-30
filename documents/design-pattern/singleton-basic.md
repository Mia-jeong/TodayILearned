<h1><a name="header-n220" class="md-header-anchor md-print-anchor" href="af://n220"> </a><span>Singleton</span></h1>
<p>&nbsp;</p>
<h3><a name="header-n222" class="md-header-anchor md-print-anchor" href="af://n222"> </a><span>1. Singleton Pattern</span></h3>
<p><span>Singleton pattern이란 하나의 클래스에 대하여 시스템 전체에서 하나의 instance만 사용하도록 하는 패턴이다. DB 의 connection을 위한 객체를 생성할때 자주 쓰인다.</span></p>
<p>&nbsp;</p>
<h3><a name="header-n225" class="md-header-anchor md-print-anchor" href="af://n225"> </a><span>2. Basic Singleton</span></h3>
<p><span>가장 기본적인 Singleton 은 다음과 같다.</span></p>
<p>&nbsp;</p>
<pre><code class='language-java' lang='java'>public class BasicSingleton implements Serializable {
    private BasicSingleton(){

    }
    private static final BasicSingleton INSTANCE = new BasicSingleton();

    public static BasicSingleton getInstance(){
        return INSTANCE;
    }

    private int value = 0;

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }

}

</code></pre>
<p><span>해당 소스를 보면 constructor가 private 으로 설정 되어 있는 것을 확인 할 수 있다. 따라서 해당 constructor를 외부에서 접근 할 수가 없다. 그렇기 때문에 우리는 getInstance() 라는 전역(static)함수를 만들어서 객체를 생성해야 한다. getInstance() 함수의 return 값을 보면 INSTANCE라는 상수를 리턴하는 것을 확인 할 수 있는데 해당 변 수는 final로 생성되어있기 때문에 변경 할 수가 없다. 그렇기 때문에 우리는 해당 객체를 한 번만 생성 할 수 있는 것이다.</span></p>
<p>&nbsp;</p>
<pre><code class='language-java' lang='java'>class Demo{

    public static void main(String[] args) throws  Exception {
        BasicSingleton singleton = BasicSingleton.getInstance();
        singleton.setValue(111);
        BasicSingleton singleton2 = BasicSingleton.getInstance();
        singleton2.setValue(222);

        System.out.println(singleton == singleton2);
        System.out.println(singleton.getValue());
        System.out.println(singleton2.getValue());
    }
}
</code></pre>
<p><span>위의 소스를 실행 시키면 다음과 같은 결과 값을 없을 수 있다.</span></p>
<p><span>&lt;결과&gt;</span></p>
<pre><code class='language-html' lang='html'>true
222
222
</code></pre>
<p>&nbsp;</p>
<p><span>*하지만 위의 소스는 reflection과 Serialization을 할때 여러개의 instance를 생성시키는 문제가 생긴다.</span></p>
<p><span>(reflection과 Serialization은 나중에 다른 포스트에서 정리하겠다. 간단히 설명하자면 reflection은 구체적인 클래스를 몰라도 해당 클래스의 메소드 와 타입, 변수를 사용할 수있게 클래스를 분석하는 방법을 말하며, Serialization은 jvm의 heap메모리에 상주되어있는 java객체를 java의 외부시스템에서도 사용할 수 있도록 변환 시키고(serialization) 또 외부 시스템에서 사용된 데이터를 java의 객체로 다시 변화시키는(deserialization)을 말한다.)</span></p>
<p>&nbsp;</p>
<h3><a name="header-n239" class="md-header-anchor md-print-anchor" href="af://n239"> </a><span>3. Serialization Singleton</span></h3>
<p><span>singleton 패턴에서 Serialization이 생성할 수 있는 문제점을 살펴보자.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>문제 코드</span></p>
</blockquote>
<p>&nbsp;</p>
<p><span>우선 BasicSingleton 클래스를 다음과 같이 Serialization을 implements하는 클래스로 변경 시켜 보자.</span></p>
<pre><code class='language-java' lang='java'>public class BasicSingleton implements Serializable {
    private BasicSingleton(){

    }

    private static final BasicSingleton INSTANCE = new BasicSingleton();

    public static BasicSingleton getInstance(){
        return INSTANCE;
    }

    private int value = 0;

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }

}
</code></pre>
<p>&nbsp;</p>
<p><span>이 후, Demo Class에 다음과 같이 saveToFile(Serialize) 와  readFromFile(Deserialize)를 하는 함수를 추가해 보자.</span></p>
<pre><code class='language-java' lang='java'>class Demo{

    static void saveToFile(BasicSingleton singleton, String fileName) throws  Exception
    {
        try(FileOutputStream fileOut = new FileOutputStream(fileName);
            ObjectOutputStream out = new ObjectOutputStream(fileOut)
        ){
            out.writeObject(singleton);
        }
    }

    static BasicSingleton readFromFile(String fileName) throws Exception{
        try(FileInputStream fileIn = new FileInputStream(fileName);
            ObjectInputStream in = new ObjectInputStream(fileIn)){
            return (BasicSingleton) in.readObject();
        }
    }
    public static void main(String[] args) throws  Exception {
        BasicSingleton singleton = BasicSingleton.getInstance();
        singleton.setValue(111);

        String filename = &quot;singleton.bin&quot;;
        saveToFile(singleton, filename);
        singleton.setValue(222);

        BasicSingleton singleton2 = readFromFile(filename);

        System.out.println(singleton == singleton2);
        System.out.println(singleton.getValue());
        System.out.println(singleton2.getValue());
    }
}
</code></pre>
<p><span>마지막으로 main method 를 실행 시키면 다음과 같이 singleton 패턴이 파괴된 것을 알 수 있다. 즉 컴파일러가 serialize를 하면서 새로운 instance를 생성했기 때문이다.</span></p>
<p>&nbsp;</p>
<p><span>&lt;결과&gt;</span></p>
<pre><code class='language-html' lang='html'>false
222
111
</code></pre>
<p>&nbsp;</p>
<blockquote><p><span>해결책</span></p>
</blockquote>
<p>&nbsp;</p>
<p><span>위의 문제를 해결하는 방법은 다음과 같다. 바로 BasicSingleton에 다음과 같이 readResolve() method를 추가시켜주면 된다.</span></p>
<pre><code class='language-java' lang='java'>public class BasicSingleton implements Serializable {
    private BasicSingleton(){

    }

    private static final BasicSingleton INSTANCE = new BasicSingleton();

    public static BasicSingleton getInstance(){
        return INSTANCE;
    }

    private int value = 0;

    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }
		//add this method
    protected  Object readResolve() {
        return INSTANCE;
    }

}
</code></pre>
<p><span>ObjectInputStream이 Object를 읽기 시작할때 먼저 해당 Object가 readResolve함수를 가지고 있는지 체크하고 만약 해당 Object가 readResolve함수를 가지고 있다면 그 함수를 실행시켜 stream이 포함하고 있는 Object가 INSTANCE(우리가 작성한 readResolve의 return 값) 를 가리키도록 하고 해당 인스턴스를 리턴해주기 때문이다.</span></p>
<p>&nbsp;</p>
<p><span>이제 다음 소스를 실행시키면 우리가 원하는 결과 값을 얻을 수 있다.</span></p>
<pre><code class='language-java' lang='java'>    public static void main(String[] args) throws  Exception {
        BasicSingleton singleton = BasicSingleton.getInstance();
        singleton.setValue(111);

        String filename = &quot;singleton.bin&quot;;
        saveToFile(singleton, filename);
        singleton.setValue(222);

        BasicSingleton singleton2 = readFromFile(filename);

        System.out.println(singleton == singleton2);
        System.out.println(singleton.getValue());
        System.out.println(singleton2.getValue());

        Class c = Class.forName(&quot;java.lang.String&quot;);

        System.out.println(c);
    }
</code></pre>
<p>&nbsp;</p>
<p><span>&lt;결과&gt;</span></p>
<pre><code class='language-html' lang='html'>true
222
222
</code></pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3><a name="header-n258" class="md-header-anchor md-print-anchor" href="af://n258"> </a><span>4. Static Block Singleton</span></h3>
<p><span>만약 우리가 생성하는 class 의 instructor가 Exception 을 throws하면 어떻게 해야 할까? 일단 코드를 작성해서 확인 해보자.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>Exception을 throws 하는 constructor</span></p>
</blockquote>
<p>&nbsp;</p>
<pre><code class='language-java' lang='java'>public class StaticBlockSingleton {

    private StaticBlockSingleton() throws IOException {
        System.out.println(&quot;Singleton is initializing&quot;);
        File.createTempFile(&quot;.&quot;, &quot;.&quot;);
    }

    //error
    private final static StaticBlockSingleton instance = new SingleSelectionModel();

    public static StaticBlockSingleton getInstance(){
        return instance;
    }
}
</code></pre>
<p>&nbsp;</p>
<p><span>다음과 같은 코드를 작성하면 instance 상수선언 부분이 에러가 발생 할것이다. 에러의 내용은 다음과 같다</span></p>
<p><span>&#39; StaticBlockSingleton is abstract cannot be instantiated&#39; 즉 throws Exception 때문에 해당 클래스의 인스턴스를 생성할 수 없다.</span></p>
<p>&nbsp;</p>
<p><span>그렇다면 우리는 해당 클래스를 singleton으로 만들기 위해서 어떻게 해야할까?</span></p>
<p><span>다음과 같이 클래스 초기화 블럭(static{})을 선언해 주면 된다.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>클래스 초기화 블럭 추가를 통해 singleton생성</span></p>
</blockquote>
<p>&nbsp;</p>
<pre><code class='language-java' lang='java'>public class StaticBlockSingleton {
		//클래스 초기화 블럭 : 클래스가 처음 로딩될때 실행되는 블럭
    static {
        try{
            instance = new StaticBlockSingleton();
        }catch(Exception e) {
            System.err.println(&quot;failed to create singleton&quot;);
        }
    }

    private StaticBlockSingleton() throws IOException {
        System.out.println(&quot;Singleton is initializing&quot;);
        File.createTempFile(&quot;.&quot;, &quot;.&quot;);
    }

    private static StaticBlockSingleton instance;

    public static StaticBlockSingleton getInstance(){
        return instance;
    }
}
</code></pre>
<p><span>다음과 같이 클래스 초기화 블럭을 추가해주면 해당 클래스를 singleton 패턴으로 호출 할 수 있게 된다.</span></p>

