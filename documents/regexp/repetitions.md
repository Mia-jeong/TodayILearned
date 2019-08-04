<h1><a name="header-n267" class="md-header-anchor md-print-anchor" href="af://n267"> </a><span>Regular Expression - Repetitions</span></h1>
<p><code>@Hackkerank</code><span>에서 Repetitions에 관한 Regular Expression 문제를 풀어 보았다.</span></p>
<h5><a name="header-n269" class="md-header-anchor md-print-anchor" href="af://n269"> </a><span>1. {x}: {x} 앞에 단어 혹은 단어 그룹[]과 정확하게 x 번 매치 하는 문자열을 구한다.</span></h5>
<p><span>\w{4}   &gt;  </span><code>H_ck</code></p>
<p><span>[xyz]    &gt;  </span><code>xyzxz</code><span> </span></p>
<p><span>[\d{4}] &gt;  </span><code>1423</code><span> </span></p>
<blockquote><p><span>Matching {x} Repetitions</span></p>
</blockquote>
<p><span>다음조건과 만족하는 문자열을 구하는 정규식을 작성하여라 .</span></p>
<ul>
<li><span>문자열은 반드시 길이가 </span><code>45</code><span>여야 한다.</span></li>
<li><span>40번째 문자열까지는 만드시 </span><code>문자</code><span> 혹은 </span><code>짝수</code><span>로 구성되어 있어야 한다.</span></li>
<li><span>41~45번째 문자열은 </span><code>홀수</code><span>이거나 </span><code>whitespace</code><span>여야 한다.</span></li>

</ul>
<pre><code class='language-pseudocode' lang='pseudocode'>^[a-zA-Z02468]{40}[13579\s]{5}$
</code></pre>
<p>&nbsp;</p>
<h5><a name="header-n285" class="md-header-anchor md-print-anchor" href="af://n285"> </a><span>2. {x,y}: {x,y} 앞에 단어 혹은 단어 그룹[]과 x~y번 매치하는 문자열을 구한다.</span></h5>
<p><span>\w{1,4}\d{4,}</span>
<code>Hk132156153186131</code>
<code>Hack1021</code></p>
<ul>
<li><span>w{3, 5} : </span><code>모든 단어</code><span>들에 관하여3~5번 매치될 수 있다.</span></li>
<li><span>[xyz]{5,}: </span><code>x, y, z</code><span> 들 중 5번 이상 매치 될 수 있다.</span></li>
<li><span>\d{1, 4}: </span><code>숫자</code><span>와 1~4번까지 매치될 수 있다.</span></li>

</ul>
<blockquote><p><span>Matching {x, y} Repetitions</span></p>
</blockquote>
<p><span>다음조건과 만족하는 문자열(S)을 구하는 정규식을 작성하여라.</span></p>
<ul>
<li><span>S는 는 반드시 </span><code>숫자</code><span>로 시작하며 숫자는 갯수가 1~2 개 까지 나올 수 있다..</span></li>
<li><span>이후, S는 3 번 이상의</span><code>문자</code><span>가 나와야한다.</span></li>
<li><span>S의 끝으로는 0~3번까지 </span><code>.</code><span>가 올 수 있다.</span></li>

</ul>
<pre><code class='language-pseudocode' lang='pseudocode'>^\d{1,2}[a-zA-Z]{3,}[\.]{0,3}
</code></pre>
<p>&nbsp;</p>
<h5><a name="header-n306" class="md-header-anchor md-print-anchor" href="af://n306"> </a><span>3. * : *는 앞에 단어 혹은 단어 그룹[] 과 0번 혹은 그 이상 매치하는 문자열을 구한다.</span></h5>
<p><span>Ab*s</span>
<code>As</code><span>  (b가 0번)</span>
<code>Abbbbs</code><span> (b가 4번)</span></p>
<ul>
<li><span>w* : 문자</span><code>w</code><span>와 0번 혹은 그 이상 매치 할 수 있다.</span></li>
<li><span>[xyz]* :</span><code>x, y</code><span>혹은 </span><code>z</code><span>와 0번 혹은 그 이상 매치 할 수 있다.</span></li>
<li><span>\d*: 어떤 </span><code>숫자</code><span>와도 0번 혹은 그 이상 매치 할 수 있다.</span></li>

</ul>
<p>&nbsp;</p>
<blockquote><p><span>Matching Zero Or More Repetitions</span></p>
</blockquote>
<p><span>다음조건과 만족하는 문자열(S)을 구하는 정규식을 작성하여라.</span></p>
<ul>
<li><span>S는 2개 이상의 </span><code>숫자</code><span>들로 시작해야한다.</span></li>
<li><span>이후, S는 0개 이상의 갯수의 </span><code>소문자</code><span>들로 구성 되어야 한다.</span></li>
<li><span>S는 0개 이상의  </span><code>대문자</code><span>들로 끝이나야 한다.</span></li>

</ul>
<pre><code class='language-pseudocode' lang='pseudocode'>^\d{2,}[a-z]*[A-Z]*$
</code></pre>
<p>&nbsp;</p>
<h5><a name="header-n328" class="md-header-anchor md-print-anchor" href="af://n328"> </a><span>4. + : +는 앞에 단어 혹은 단어 그룹[] 과 1번 혹은 그 이상 매치하는 문자열을 구한다.</span></h5>
<p><span>Ab+s</span>
<code>Abbbbs</code></p>
<ul>
<li><span>w+: 문자 </span><code>w</code><span>와 1번 혹은 그 이상 매치 할 수 있다.</span></li>
<li><span>[xyz]+ :</span><code>x, y</code><span> 혹은 </span><code>z</code><span> 와 1번 혹은 그 이상 매치 할 수 있다.</span></li>
<li><span>\d+: 어떤 </span><code>숫자</code><span>와도 1번 혹은 그 이상 매치 할 수 있다.</span></li>

</ul>
<p>&nbsp;</p>
<blockquote><p><span>Matching One of More Repetitions</span></p>
</blockquote>
<p><span>다음조건과 만족하는 문자열(S)을 구하는 정규식을 작성하여라.</span></p>
<ul>
<li><span>S는 1개 이상의 </span><code>숫자</code><span> 들로 시작해야 한다.</span></li>
<li><span>이후 , S는 1개 이상의 </span><code>대문자</code><span> 들로 구성되어 있어야 한다.</span></li>
<li><span>S는 1개혹은 그 이상의 </span><code>소문자</code><span> 들로 끝이 나야 한다.</span></li>

</ul>
<pre><code class='language-pseudocode' lang='pseudocode'>^\d+[A-Z]+[a-z]+$
</code></pre>
<p>&nbsp;</p>
<h5><a name="header-n350" class="md-header-anchor md-print-anchor" href="af://n350"> </a><span>5.$ 앞의 단어 혹은 단어 그룹[] 으로 해당 문자열이 끝이난다.</span></h5>
<p><span>\w*s$</span>
<code>ChallengesHints</code></p>
<p>&nbsp;</p>
<blockquote><p><span>Matching Ending Items</span></p>
</blockquote>
<p><span>다음조건과 만족하는 문자열(S)을 구하는 정규식을 작성하여라.</span></p>
<ul>
<li><span>S는 반드시</span><code>소문자</code><span>와 </span><code>대문자</code><span>로 구성되어야 한다.</span></li>
<li><span>S는 반드시 </span><code>s</code><span> 로 끝이 나야 한다.</span></li>

</ul>
<pre><code class='language-pseudocode' lang='pseudocode'>^[a-zA-Z]*s$
</code></pre>
<p>&nbsp;</p>
