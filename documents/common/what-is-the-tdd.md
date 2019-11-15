<h1><a name="header-n258" class="md-header-anchor md-print-anchor" href="af://n258"> </a><span>테스트 주도 개발 (TDD)</span></h1>
<blockquote><p><span>목표주도 개발</span></p>
</blockquote>
<p><span>말그대로 테스트가 개발을 주도한다는 것을 의미 한다. 즉, 목표주도 개발을 하는 것을 말한다.</span></p>
<p><span>테스트를 하기위해서는 사용자 입장으로 사용해 보아야 한다. 따라서 사용자 중심 개발이라고 부르기도 한다.</span></p>
<p><span>또한 우리가 만드는 코드는 객체들끼리 서로 연관되어 사용되므로 인터페이스 주도 개발이라고도 부른다.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>올바르게 작동, 깔끔한 코드</span></p>
</blockquote>
<p><span>먼저 올바르게 작동하는 코드를 만 든 후, Refactoring 한다</span></p>
<p><span>Refactoring 란 올바르게 작동하면서 코드만을 바꾸는 것을 의미한다. 이렇게 Refactoring 하기 위해서는 Test code가 필요하다.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>Test First</span></p>
</blockquote>
<p><span>보통 개발을 하고 난 후 테스트를 한다고 생각하지만 테스트 코드를 먼저 작성하고 코드를 작성해야 TDD목적성을 달성 하는 것이다.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>TDD Cycle : Red , Green, Refactoring</span></p>
</blockquote>
<p>&nbsp;</p>
<ol>
<li><span>Red : 실패하는 테스트를 의미한다. (Ex. 아무것도 안하고 테스트 코드를 작성하는 경우 당연히 테스트는 실패 )</span></li>
<li><span>Green: 올바르게 작동하는 코드를 작성.</span></li>
<li><span>Refactoring: 코드가 경우에 따라 실패하는 경우를 방지하기 위해 Refactoring </span></li>

</ol>
<p>&nbsp;</p>
<blockquote><p><span>미래의 고통을 미리 예방 하는것(예방접종 같은것)</span></p>
</blockquote>
<p><span>일일이 테스트 하면서 코드를 작성하는건 개발을 할 당시에는 번거로운 일이 될 수 있으나 미래에 테스트코드가 없이 리팩토링을 할 끔찍한 상황에 마주치지 않으려면 아주 좋은 습관이다.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>계속해서 훈련이 필요한다.</span></p>
</blockquote>
<p><span>올바른 테스트 코드를 작성하기 위해서는  계속해서 RED &gt; GREEN &gt; REFACTORING 을 통한 연습이 필요하다.</span></p>
<p>&nbsp;</p>
<blockquote><p><span>실습)</span></p>
</blockquote>
<p>&nbsp;</p>
<ol>
<li><span>Restaurant Domain 작성</span></li>

</ol>
<pre><code class='language-java' lang='java'>public class Restaurant {
      public String getName() {
        return &quot;&quot;;
    }
}
</code></pre>
<ol start='2' >
<li><span>Testcode 작성 - RED <br> 참고로 1번 Restaurant domain에 오른쪽 마우스 클릭 후 `Go to` 메뉴에서 `Test`를 클릭하면 테스트를 자동으로 생성 할수 있다.</span></li>

</ol>
<pre><code class='language-java' lang='java'>public class RestaurantTests {
    @Test
    public void creation() {
        assertThat(restaurant.getName(), is(&quot;Great Restaurant&quot;));
    }
}
</code></pre>
<p><span>해당 코드는 restaurant에 getName이 없으므로 통과하지 못한다 &gt; Red!</span></p>
<ol start='3' >
<li><span>올바르게 작동하기 위한 기능 추가 -Green</span></li>

</ol>
<pre><code class='language-java' lang='java'>public class Restaurant {
    public String getName() {
        return &quot;Great Restaurant&quot;;
    }
}
</code></pre>
<p><span>Restaurant을 다음과 같이 고치고 테스트를 작동시키면 통과 될것이다 </span></p>
<ol start='4' >
<li><span>Refactoring</span></li>

</ol>
<pre><code class='language-java' lang='java'>public class Restaurant {
    private final String name;
    public Restaurant(String name) {
        this.name = name;
    }
    public String getName() {
        return this.name;
    }
}
</code></pre>
<pre><code class='language-java' lang='java'>public class RestaurantTests {
    @Test
    public void creation() {
        Restaurant restaurant = new Restaurant(&quot;Great Restaurant&quot;);
        assertThat(restaurant.getName(), is(&quot;Great Restaurant&quot;));

    }
}
</code></pre>
<p><span>마지막으로 코드를 리팩토링 하자.</span></p>
<p><span>이런식으로 Red 테스트 케이스 작성 &gt; 테스트 통과가 통과될수 있는 Green코드 작성 &gt; Refactoring 을 통해 개발 하는것이 바로 TDD이다</span></p>
<p>&nbsp;</p>
<p><span>*참고로 SpringBoot와 Junit4를 사용하였다.</span></p>
