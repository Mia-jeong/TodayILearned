<h1><a class="md-header-anchor md-print-anchor" href="af://n188" name="header-n188"> </a><span>Prototype</span></h1>
<h3><a class="md-header-anchor md-print-anchor" href="af://n189" name="header-n189"> </a><span>1.Prototype Pattern?</span></h3>
<p><span>Prototype Pattern 이란 본래의 object로부터 deep copy(not shallow copy)를 통해 새로운 Object를 만들어 내는 패턴이다. 비슷한 object를 지속적으로 생성해야 할 때 유용하게 사용된다.</span></p>
<p>&nbsp;</p>
<h3><a class="md-header-anchor md-print-anchor" href="af://n192" name="header-n192"> </a><span>2. Clonable을 통한 Copy</span></h3>
<p>&nbsp;</p>
<blockquote>
<p><span>Shallow copy</span></p>
</blockquote>
<p>&nbsp;</p>
<pre class="language-java"><code>class Address  {
    public String streetName;
    public int houseNumber;

    public Address(String streetName, int houseNumber) {
        this.streetName = streetName;
        this.houseNumber = houseNumber;
    }

    @Override
    public String toString() {
        return "Address{" +
                "streetName='" + streetName + '\'' +
                ", houseNumber=" + houseNumber +
                '}';
    }
}

class Person
{
    public String [] names;
    public Address address;

    public Person(String[] names, Address address) {
        this.names = names;
        this.address = address;
    }

    @Override
    public String toString() {
        return "Person{" +
                "names=" + Arrays.toString(names) +
                ", address=" + address +
                '}';
    }
}

</code></pre>
<p><span>다음과 같이 Address클래스와 이를 변수로 가지고 있는 Person클래스를 생성해 보자. 이후 다음과 같은 로직을 실행시켜보자.</span></p>
<p>&nbsp;</p>
<pre class="language-java"><code>public class Prototype {
    public static void main(String[] args) {
        Person john = new Person(new String[]{"John", "Smith"}, new Address("Gangnam Road", 1029));
        Person jane = john; //copy, so to speak it's shallow copy
        jane.names[0] = "Jane";
        jane.address.houseNumber = 1004; //they both share the same data, cuz they refer to same object

        System.out.println(john);
        System.out.println(jane);
    }
}
</code></pre>
<p><span>위의 코드를 실행시키면 john과 jane은 똑같은 값을 출력할 것이다 왜냐하면 john과 jane은 같은 object의 메모리 주소를 참조하고 있기 때문이다 우리는 이걸 shallow copy라고 한다. 그렇다면 deep copy를 하기 위해서는 어떻게 해야 할까?</span></p>
<p><span>바로 clonable을 사용해보자 🙋&zwj;♀️</span></p>
<p>&nbsp;</p>
<blockquote>
<p><span>Clonable을 사용 한 Deep Copy</span></p>
</blockquote>
<p>&nbsp;</p>
<p><span>우선 Address 클래스에 다음과 같이 Clonable 인터페이스를 implements를 시켜주고 clone() 함수를 오버라이드 시켜주자</span></p>
<pre class="language-java"><code>class Address implements Cloneable {
    public String streetName;
    public int houseNumber;

    public Address(String streetName, int houseNumber) {
        this.streetName = streetName;
        this.houseNumber = houseNumber;
    }

    @Override
    public String toString() {
        return "Address{" +
                "streetName='" + streetName + '\'' +
                ", houseNumber=" + houseNumber +
                '}';
    }

    //deep copy
    @Override
    public Object clone() throws CloneNotSupportedException {
        return new Address(streetName, houseNumber);
    }
}
</code></pre>
<p>&nbsp;</p>
<p><span>(참고)</span></p>
<p><span>오버라이드 된 clone() 함수의 기본 값은 원래 다음과 같다.</span></p>
<pre class="language-java"><code>    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
</code></pre>
<p>&nbsp;</p>
<p><span>이후, Person 클래스에도 다음과 같은 작업을 해주자.</span></p>
<p>&nbsp;</p>
<pre class="language-java"><code>class Person implements Cloneable
{
    public String [] names;
    public Address address;

    public Person(String[] names, Address address) {
        this.names = names;
        this.address = address;
    }

    @Override
    public String toString() {
        return "Person{" +
                "names=" + Arrays.toString(names) +
                ", address=" + address +
                '}';
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return new Person(names.clone(), (Address) address.clone());
    }
}
</code></pre>
<p>&nbsp;</p>
<p><span>이제 마지막으로 우리가 원했던 deep copy를 실행시켜보자.</span></p>
<p>&nbsp;</p>
<pre class="language-java"><code>public class Prototype {
    public static void main(String[] args) throws Exception {
        Person john = new Person(new String[]{"John", "Smith"}, new Address("Gangnam Road", 1029));
        Person jane = (Person) john.clone();

        jane.names[0] = "Jane";
        jane.address.houseNumber = 1004;
        System.out.println(john);
        System.out.println(jane);
    }
}
</code></pre>
<p>&nbsp;</p>
<p><span>이제 결과 값은 원했던 대로 john과 jane이 각각 다르게 출력될 것이다.</span></p>
<pre class="language-java"><code>Person{names=[John, Smith], address=Address{streetName='Gangnam Road', houseNumber=1029}}
Person{names=[Jane, Smith], address=Address{streetName='Gangnam Road', houseNumber=1004}}
</code></pre>
<p>&nbsp;</p>
<blockquote>
<p><span>Deep copy를 할 때 웬만하면 Clonable을 사용하지 말자.</span></p>
</blockquote>
<p><span>Deep copy를 할씨 Clonable을 사용하는 것은 사실 그다지 추천되는 방법은 아니다. 왜냐하면 Clonable 함수는 clone method에 관하여 정확하게 언급하고 있지도 않을 뿐더러 clone의 default 결과 값은 shallow copy이기 때문이다. 따라서 deep copy를 원하는 경우 다른 방식으로 하는 것이 좋다.</span></p>
<p>&nbsp;</p>
<h3><a class="md-header-anchor md-print-anchor" href="af://n229" name="header-n229"> </a><span>3. Constructor을 이용한 Deep copy</span></h3>
<p><span>constructor을 이용하여 Deep copy를 해보자.</span></p>
<blockquote>
<p><span>Address Class</span></p>
</blockquote>
<p>&nbsp;</p>
<pre class="language-java"><code>class Address{
    public String streetAddress, city, country;
		
  	// constructor 1. 
    public Address(String streetAddress, String city, String country) {
        this.streetAddress = streetAddress;
        this.city = city;
        this.country = country;
    }

    // constructor 2. Deep copy
    public Address(Address other){
        this(other.streetAddress, other.city, other.country);
    }

    @Override
    public String toString() {
        return "Address{" +
                "streetAddress='" + streetAddress + '\'' +
                ", city='" + city + '\'' +
                ", country='" + country + '\'' +
                '}';
    }
}
</code></pre>
<p><span>위의 소스를 보자. constructor 2를 살펴보면 인자로 Address를 받아 해당 값을 통해 현재 클래스의 인스턴스를 새로 생성해 주는 것을 알 수 있다. 이와 같은 방식을 Constructor를 이용한 Deep copy라고 한다.</span></p>
<p><span>이제, Employee 클래스도 다음과 같은 방법으로 생성 해주자.</span></p>
<p>&nbsp;</p>
<blockquote>
<p><span>Employee Class</span></p>
</blockquote>
<p>&nbsp;</p>
<pre class="language-java"><code>class Employee{
    public String name;
    public Address address;

    public Employee(String name, Address address) {
        this.name = name;
        this.address = address;
    }

    public Employee(Employee other){
        this(other.name, new Address(other.address));
    }

    @Override
    public String toString() {
        return "Employee{" +
                "name='" + name + '\'' +
                ", address=" + address +
                '}';
    }
}
</code></pre>
<p>&nbsp;</p>
<blockquote>
<p><span>실행</span></p>
</blockquote>
<p>&nbsp;</p>
<pre class="language-java"><code>public class Prototype {
    public static void main(String[] args) {
        Employee john = new Employee("John", new Address("Gangnam Road", "Seoul", "KR"));

        Employee hannah = new Employee(john);
        hannah.name = "hannah";
        System.out.println(john);
        System.out.println(hannah);
    }
}
</code></pre>
<p><span>위의 소스를 실행시켜보면 john과 같은 주소를 가고 hannah라는 이름을 가진 hannah클래스가 생성된 것을 확인할 수 있다.</span></p>
<p><span>&lt;결과 값&gt;</span></p>
<pre class="language-java"><code>Employee{name='John', address=Address{streetAddress='Gangnam Road', city='Seoul', country='KR'}}
Employee{name='hannah', address=Address{streetAddress='Gangnam Road', city='Seoul', country='KR'}}
</code></pre>
<p>&nbsp;</p>
<p><span>Clonable의 clone() method보다 Constructor를 이용한 Copy는 좀 더 명백하게 Deep copy method를 알려주고 있기 때문에 전자보다는 후자를 사용하는 것이 좋다.</span></p>
<p><span>하지만 copy constructor의 가장 큰 문제점 중 하나는 모든 type 하나하나를 가진 copy constructor를 빌드해야 한다는 것이다. 즉 Person과 Address처럼 연결되어있는 타입이 20개 이상이라고 생각해보자. 그럼 우리는 20개의 copy constructor를 생성해야 한다. 😱 그렇지 않으면 deep copy가 아닌 shallow copy가 될 것이기 때문이다. 이러한 문제를 해결하기 위해 우리는 serialization를 사용할 수 있다.</span></p>
<p>&nbsp;</p>
<h3><a class="md-header-anchor md-print-anchor" href="af://n254" name="header-n254"> </a><span>4.Serialization</span></h3>
<p><span>우리가 복제하고 싶은 클래스가 여러 클래스와 엮어 있을 경우 deep copy를 하기 위해서는 SerializationUtils를 사용하면 된다.</span></p>
<p>&nbsp;</p>
<blockquote>
<p><span>복제할 클래스</span></p>
</blockquote>
<p>&nbsp;</p>
<p><span>다음과 같이 복제할 클래스 Foo를 만들어 보자.</span></p>
<pre class="language-java"><code>class Foo implements Serializable{
    public int stuff;
    public String whatever;

    public Foo(int stuff, String whatever) {
        this.stuff = stuff;
        this.whatever = whatever;
    }

    @Override
    public String toString() {
        return "Foo{" +
                "stuff=" + stuff +
                ", whatever='" + whatever + '\'' +
                '}';
    }
}
</code></pre>
<p><span>다음은 stuff와 whatever변수를 가지고 있는 평범한 Foo 클래스이다. 해당 클래스 Serializable을 implements 시켜주자.</span></p>
<p>&nbsp;</p>
<blockquote>
<p><span>Deep copy</span></p>
</blockquote>
<p>&nbsp;</p>
<p><span>이제 생성한 Foo를 SerializationUtils를 통해 deep copy 해보자.</span></p>
<pre class="language-java"><code>public class SerializationPrototype {
    public static void main(String[] args) {
        Foo foo = new Foo(42, "swimming");
        Foo foo2 = (Foo) SerializationUtils.roundtrip(foo);
        //만약 roundtrip이 안 될 경우
      	// Foo foo2 = (Foo) SerializationUtils.deserialize(SerializationUtils.serialize(foo));

        foo2.whatever = "Skydiving";
        System.out.println(foo);
        System.out.println(foo2);

    }
}
</code></pre>
<p><span>위와 같이 SerializationUtils을 사용한다면 아무리 연결된 클래스들이 많아도 각각의 클래스들을 모두 deep copy 할 것이다.</span></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>(참고) 직렬화 &gt; <a href="http://woowabros.github.io/experience/2017/10/17/java-serialize.html" target="_blank" rel="noopener">링크</a></p>
