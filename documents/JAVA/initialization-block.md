<h1><a name="header-n183" class="md-header-anchor md-print-anchor" href="af://n183"> </a><span>초기화 블럭(initialization Block)</span></h1>
<p>&nbsp;</p>
<h3><a name="header-n185" class="md-header-anchor md-print-anchor" href="af://n185"> </a><span>1. 초기화 블럭이란?</span></h3>
<p><span>초기화 블럭이란 클래스가 생성될때 무조건 수행되는 블럭을 의미한다. 이러한 초기화블럭에는 두가지 종류가 있는데 다음과 같다.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>종류</span></p>
</blockquote>
<figure><table>
<thead>
<tr><th><span>클래스 초기화 블럭</span></th><th><span>인스턴스 초기화 블럭</span></th></tr></thead>
<tbody><tr><td><span>클래스가 처음 로딩될때 한 번만 수행 되는 블럭을 의미한다.</span></td><td><span>인스턴스가 생성될 때마다 수행 되는 블럭을 의미 한다.</span></td></tr></tbody>
</table></figure>
<p><span>이둘을 각각 클래스 변수의 초기화가 복잡하거나 인스턴스 변수의 초기화가 복잡할 경우, 또한 중복코드를 줄이기 위해 사용 된다.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>형태</span></p>
</blockquote>
<p>&nbsp;</p>
<p><span>클래스 초기화 블럭과 인스턴스 초기화 블럭은 각각 다음과 같은 형태로 선언 된다. </span></p>
<pre><code class='language-java' lang='java'>class Example{
	static {
		System.out.println(&quot;클래스 초기화 블럭&quot;);
	}
	
	{ System.out.println(&quot;인스턴스 초기화 블럭&quot;);}
}
</code></pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3><a name="header-n206" class="md-header-anchor md-print-anchor" href="af://n206"> </a><span>2.초기화 블럭 활용</span></h3>
<p>&nbsp;</p>
<blockquote><p><span>중복된 문구를 가지고 있는 코드</span></p>
</blockquote>
<pre><code class='language-java' lang='java'>class Coffee{
  String name;
  int amount;
	public Coffee(){
    System.out.println(&quot;맛있는 커피&quot;)
    name = &quot;아메리카노&quot;;
   	amount = 1;
  }
  
  public Coffee(String name, int amount){
    System.out.println(&quot;맛있는 커피&quot;)
    name = name;
   	amount = amount;
  }
}
</code></pre>
<p><span>위의 코드를 보면 &quot;맛있는 커피&quot; 라는 문구가 각 생성자 마다 중복 된다. 이럴 때 우리는 인스턴스 초기화 블럭을 통해 중복을 제거 할 수 있다.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>인스턴스 클래스 초기화를 통한 중복 제거</span></p>
</blockquote>
<pre><code class='language-java' lang='java'>class Coffee{
    String name;
    int amount;

    { System.out.println(&quot;맛있는 커피&quot;);}

    public Coffee(){
        name = &quot;아메리카노&quot;;
        amount = 1;
    }

    public Coffee(String name, int amount){
        this.name = name;
        this.amount = amount;
    }
}

</code></pre>
<p><span>다음과 같이 인스턴스 클래스 초기화 블럭을 통해 중복되는 코드를 분리 할 수 있다. 클래스 초기화 블럭은 해당 객체의 인스턴스를 실행 시킬때마다 해당 블럭을 실행 시키기 때문이다. </span></p>
<p>&nbsp;</p>
<blockquote><p><span>클래스 초기화 블럭</span></p>
</blockquote>
<p><span>반면 static 블럭, 즉 클래스 초기화 블럭은 클래스가 로딩될때 하번만 실행 시킨다.</span></p>
<pre><code class='language-java' lang='java'>class Coffee{
    String name;
    int amount;

    static { System.out.println(&quot;Class loading...&quot;);}

    { System.out.println(&quot;맛있는 커피&quot;);}

    public Coffee(){
        name = &quot;아메리카노&quot;;
        amount = 1;
    }

    public Coffee(String name, int amount){
        this.name = name;
        this.amount = amount;
    }
}

</code></pre>
<p>&nbsp;</p>
<p><span>따라서 위의 코드처럼 static블럭을 추가 한 후 아래의 코드를 실행 시키면 다음과 같은 결과를 얻을 수 있다.</span></p>
<pre><code class='language-java' lang='java'>class Demo{
  public static void main(String args[]){
    Coffee c1 = new Coffee();
    Coffee c2 = new Coffee(&quot;카페라떼&quot;, 2);
  }
}
</code></pre>
<p>&nbsp;</p>
<p><span>&lt;결과&gt;</span></p>
<pre><code class='language-html' lang='html'>Class loading...    
맛있는 커피
맛있는 커피
</code></pre>
<p>&nbsp;</p>
<p><span>보는바와 같이 클래스 초기화 블럭(Class loading..)은 한 번만 출력되고 맛있는 커피는 인스턴스가 생성될때마다 출력되는 것을 확인 할 수 있다.</span></p>
