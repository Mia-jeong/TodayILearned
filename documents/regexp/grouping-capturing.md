<h1><a name="header-n156" class="md-header-anchor md-print-anchor" href="af://n156"> </a><span>Regular Expression - Grouping and Capturing</span></h1>
<h5><a name="header-n157" class="md-header-anchor md-print-anchor" href="af://n157"> </a><span>1. \b: \b 는 한 단어의 경계에 대한 위치를 찾는다. (b=. boundary)</span></h5>
<pre><code class='language-pseu' lang='pseu'>\bcat\b
</code></pre>
<p><span>Acat</span>
<span>A </span><code>cat</code>
<code>cat</code><span> is cute</span>
<span>cats are cite</span>
<span>look at the </span><code>cat</code></p>
<blockquote><p><span>Matching word boundaries</span></p>
</blockquote>
<p><span>주어진 문자열이 다음의 조건에 준수하도록 정규식을 작성하라.</span></p>
<ul>
<li><span>모음으로 시작 되는 단어를 구하여라(대소문자 구별 X )</span></li>
<li><span>해당 단어의 길이는 얼마가 되던지 상관이 없다, 다만 단어는 반드시 문자로만 구성되어야 한다.</span></li>
<li><span>단어의 시작과 끝은 반드시 단어의 경계와 함께해야 한다.</span></li>

</ul>
<pre><code class='language-pseudocode' lang='pseudocode'>\\b[aeiouAEIOU][a-zA-Z]*\\b
</code></pre>
<p>&nbsp;</p>
<h5><a name="header-n172" class="md-header-anchor md-print-anchor" href="af://n172"> </a><span>2. () : () 는 정규식 안에 하위 패턴을 지정해서 사용할 경우 사용 된다.</span></h5>
<ul>
<li><span>(?=) : </span><code>a(?=b)</code><span> a 다음 b가 일치한다.</span></li>
<li><span>(?!): </span><code>a(?!b)</code><span> a 다음 b가 일치하지 않는다.</span></li>
<li><span>(?&lt;=): </span><code>(?&lt;=a)b</code><span> a가 일치하고 b가 일치한다.</span></li>
<li><span>(?&lt;!): </span><code>(?&lt;!a)b</code><span> a가 일치하지 않고 b가 일치한다.</span></li>

</ul>
<blockquote><p><span>Capturing &amp; Non-Capturing Groups</span></p>
</blockquote>
<p><span>주어진 문자열(S)이 다음의 조건에 준수하도록 정규식을 작성하라.</span></p>
<ul>
<li><span>주어진 문자열 S는 단어  </span><code>ok</code><span>가 3번이상 반복 되어야 한다. </span></li>

</ul>
<pre><code class='language-pse' lang='pse'>(ok){3,}
</code></pre>
<p>&nbsp;</p>
<h5><a name="header-n190" class="md-header-anchor md-print-anchor" href="af://n190"> </a><span>3.| : |는 패턴을 OR 연산을 수행 할때 사용 된다.</span></h5>
<p><span>(And|AND|And)</span>
<code>And</code><span> the award goes to</span>
<span>A </span><code>and</code><span> D Company</span></p>
<blockquote><p><span>Alternative Matching</span></p>
</blockquote>
<p><span>주어진 문자열(S)이 다음의 조건에 준수하도록 정규식을 작성하라.</span></p>
<ul>
<li><span>주어진 문자열 S는 반드시 </span><code>Mr.</code><span> , </span><code>Mrs.</code><span> ,</span><code>Ms.</code><span>,</span><code>Dr.</code><span> 혹은 </span><code>Er</code><span> 로 시작해야 한다.</span></li>
<li><span>나머지 문자열은 반드시 1개 이상의 영어 알파멧 문자들을 포함해야 한다(대 소문자 상관 없음)</span></li>

</ul>
<pre><code class='language-pseudocode' lang='pseudocode'>^(Mr|Mrs|Ms|Dr|Er)[\\.][a-zA-Z]+
</code></pre>
<p>&nbsp;</p>
