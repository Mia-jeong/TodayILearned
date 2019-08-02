<h1><a name="header-n286" class="md-header-anchor md-print-anchor" href="af://n286"> </a><span>정규식(Regexp) 개념 및 Introduction 문제 풀이</span></h1>
<p><span>그동안, 정규식을 어렴풋이 사용하다가 업무를 하면서 많이 사용하게 되어 본격적으로 공부해야 겠다고 마음을 먹었다. 그래서 오늘 부터 @Hackerrank에서 정규식 문제도 같이 풀어보기로 했다. 참고로 정규식문제를 풀 경우 언어는 </span><code>Java8</code><span> 을 사용 하였다.</span></p>
<h3><a name="header-n288" class="md-header-anchor md-print-anchor" href="af://n288"> </a><span>☀️ 정규식 이란 무엇일까?</span></h3>
<p><span>String값에서 특정한 규칙을 가진 문자나 숫자의 조합과 대응시키기 위해 사용되는 패턴이다.</span></p>
<p>&nbsp;</p>
<h3><a name="header-n291" class="md-header-anchor md-print-anchor" href="af://n291"> </a><span>✍️ 정규식 Introduction 문제 풀이</span></h3>
<h5><a name="header-n292" class="md-header-anchor md-print-anchor" href="af://n292"> </a><span>1. 구체적인 문자열 일치시키기</span></h5>
<pre><code class='language-pseudocode' lang='pseudocode'>\apple\g
</code></pre>
<p><span> </span><code>apple</code><span>, banana,  </span><code>apple</code></p>
<p>&nbsp;</p>
<h5><a name="header-n296" class="md-header-anchor md-print-anchor" href="af://n296"> </a><span>2. dot(.)을 사용하여 newLine을 제외하고 다 매칭시키기 </span></h5>
<pre><code class='language-pseudocode' lang='pseudocode'>\A.B.C.D\g
</code></pre>
<p><code>A+B-C=DE</code></p>
<blockquote><p><span> Matching Anything But a Newline</span></p>
</blockquote>
<p><span>abc.def.ghi.jkx 와 일치하는 값을 찾아라 각각의 변 수 a,b,c,d,e,f,g,h,i,j,k,x는 newLine을 제외한 어떠한 단일 문자도 될 수 있다.</span></p>
<pre><code class='language-\\pseudocode' lang='\\pseudocode'>...\\....\\....\\....
</code></pre>
<p><code>123.456.abc.def</code></p>
<p>&nbsp;</p>
<h5><a name="header-n305" class="md-header-anchor md-print-anchor" href="af://n305"> </a><span>3.\d 와 \D를 사용하여 숫자(\d)와 숫자(\D)가 아닌 문자를 매칭</span></h5>
<blockquote><p><span>Matching Digits &amp; Non-Digit Characters</span></p>
</blockquote>
<p><span>다음 패턴과 일치하는 문자열을 출력하라 xxXxxXxxxx</span></p>
<p><span>여기에서 x는 숫자를 나타내고 X는 문자를 나타낸다.</span></p>
<pre><code class='language-pseudocode' lang='pseudocode'>(\\d{2}\\D){2}\\d{4}
</code></pre>
<p><span>Today it is on </span><code>06-11-2019</code></p>
<p>&nbsp;</p>
<h5><a name="header-n313" class="md-header-anchor md-print-anchor" href="af://n313"> </a><span>4. \s 와 \S를 사용하여 white space인 것(\s)과 아닌 것(\S)을 매칭 </span></h5>
<blockquote><p><span> Matching Whitespace &amp; Non-Whitespace Character</span></p>
</blockquote>
<p><span>주어진 스트링에서 XXxXXxXX패턴과 일치하는 문장을 구하여라</span></p>
<p><span>x는 white space를 의미하고 X는 white space 가 아닌 문장을 의미한다.</span></p>
<pre><code class='language-pseudocode' lang='pseudocode'>(\\S{2}\\s{1}){2}\\S{2}
</code></pre>
<p><span> </span><code>12 11 5</code></p>
<p>&nbsp;</p>
<h5><a name="header-n321" class="md-header-anchor md-print-anchor" href="af://n321"> </a><span>5.\w와 \W를 사용하여 문자 혹은 숫자 인 것(\w)과 문자 혹은 숫자 가 아닌 것 (\W) 문자열을 구하여라.</span></h5>
<blockquote><p><span> Matching Word &amp; Non-Word Character</span></p>
</blockquote>
<p><span>주어진 스트링에서 xxxXxxxxxxxxxxXxxx 와 일치하는 문자열을 구하라.</span></p>
<p><span>여기서 x는 문자 혹은 숫자를 의미하며 X는 문자나 숫자가 아닌 것을 의미 한다.</span></p>
<pre><code class='language-pseudocode' lang='pseudocode'>\\w{3}\\W\\w{10}\\W\\w{3}
</code></pre>
<p><code>ww.hackerrank.com</code></p>
<p>&nbsp;</p>
<h5><a name="header-n329" class="md-header-anchor md-print-anchor" href="af://n329"> </a><span>6. ^와 $를 사용하여 시작글자와 끝 글자를 일치시켜보자.</span></h5>
<p><span>✓ ^ : 해당패턴이 문장의 시작글자와 일치 </span></p>
<p><span>✓ $ : 해당 패턴이 문장의 끝 글자와 일치</span></p>
<blockquote><p><span>Matching Start &amp; End</span></p>
</blockquote>
<p><span>주어진 문자열 값에서 Xxxxx. 패턴과 일치하는 문장을 구하라. </span></p>
<p><span>x는 문자를 의미하고 X는 숫자를 의미한다. 문자열은 반드시 숫자로 시작하고 .으로 끝나야 한다. 또한 무조건 길이가 6이어야 한다.</span></p>
<pre><code class='language-pseudocode' lang='pseudocode'>^\\d\\w{4}\\.$
</code></pre>
<p><code>0qwer.</code></p>
<p>&nbsp;</p>
