<h1><a name="header-n178" class="md-header-anchor md-print-anchor" href="af://n178"> </a><span>Regular Expression - Character Class </span></h1>
<p><span>오늘도 정규식을 공부하기 위해 @Hackerrank문제를 풀었다.</span></p>
<h5><a name="header-n180" class="md-header-anchor md-print-anchor" href="af://n180"> </a><span>1. []: [] 안의 글자나 문자 중 오직 한 가지만 매치 된다.</span></h5>
<p><code>[aeiou]</code><span> is vowel </span>
<code>o</code><span> is a vowel</span>
<code>e</code><span> is a vowel</span></p>
<blockquote><p><span>Matching Specific Characters</span></p>
</blockquote>
<p><span>주어진 문자열이 다음의 조건에 준수하도록 정규식을 작성하라 </span></p>
<ul>
<li><span>주어진 문자열은 반드시 6글자여야 한다.</span></li>
<li><span>첫번째 단어는 1,2 혹은 3이어야 한다.</span></li>
<li><span>두번째 단어는 1, 2 혹은 0 이어야 한다.</span></li>
<li><span>세번째 단어는 x, s  혹은 0 이어야 한다.</span></li>
<li><span>네번째 단어는 3, 0, A 혹은 a 여야 한다.</span></li>
<li><span>다섯번째 단어는 x, s 혹은 u여야 한다.</span></li>
<li><span>여섯번째 단어는 . 혹은 , 여야 한다.</span></li>

</ul>
<pre><code class='language-pseudocode' lang='pseudocode'>^[123][120][xs0][30Aa][xsu][.,]$
</code></pre>
<p>&nbsp;</p>
<h5><a name="header-n202" class="md-header-anchor md-print-anchor" href="af://n202"> </a><span>2. [^]: [^]안의 글자 빼고 어떠 한 문자와도 매치 된다.</span></h5>
<p><code>[^aeiou]</code><span> is not a vowel</span></p>
<p><code>k</code><span> is not a vowel</span>
<code>p</code><span> is not a vowel</span></p>
<blockquote><p><span>Excluding Specific Characters</span></p>
</blockquote>
<p><span>주어진 문자열이 다음의 조건에 준수하도록 정규식을 작성하라.</span></p>
<ul>
<li><span>주어진 문자열은 반드시 6글자여야 한다.</span></li>
<li><span>첫번째 단어는 (1,2,3,4,5,6,7,8,9,0)이 아니어야 한다.</span></li>
<li><span>두번째 단어는 소문자 모음인 (a, e, i, o, u) 가 아니어야 한다.</span></li>
<li><span>세번째 단어는 b,c,D,F가 아니어야 한다.</span></li>
<li><span>네번째 단어는 \r, \n, \t, \f 혹은 white space가 아니어야 한다.</span></li>
<li><span>다섯번째 단어는 대문자 A, E, I, O, U가 아니어야 한다.</span></li>
<li><span>여섯번째 단어는 . 혹은 ,가 아니어야 한다.</span></li>

</ul>
<pre><code class='language-pseudocode' lang='pseudocode'>^[^\\d][^aeiou][^bcDF][\S][^AEIOU][^.,]$
</code></pre>
<p>&nbsp;</p>
<h5><a name="header-n225" class="md-header-anchor md-print-anchor" href="af://n225"> </a><span>3. []내의 문자열 매칭 범위</span></h5>
<ul>
<li><span>[a-z] = [abcdefghijklmnopqrstuvwxyz]</span></li>
<li><span>[A-Z] = [ABCDEFGHIJKLMNOPQRATUVWXYZ]</span></li>
<li><span>[0-9] = [0123456789</span></li>
<li><span>만약 범위 앞에 ^ 을 넣으면 범위에 속하는 단어들을 제외하고 모두 매칭 될 것이다.</span></li>

</ul>
<blockquote><p><span>Matching Character Ranges</span></p>
</blockquote>
<p><span>다음 조건을 만족 시키는 정규식을 작성하라.</span></p>
<ul>
<li><span>문자열은 5글자 이상이여야 한다.</span></li>
<li><span>첫번째 단어는 반드시 소문자 영어 알파벳이어야 한다.</span></li>
<li><span>두번째 문자는 양수여야 한다(0은 양수도 음수 도 아님)</span></li>
<li><span>세번째문자는 소문자 영어 알파벳이 아니 어야 한다.</span></li>
<li><span>네번째 문자는 반드시 대문자 영어 알파벳이 아니 어야 한다.</span></li>
<li><span>다섯번재 문자는 반드시 대문자 영어 알파벳이어야 한다.</span></li>

</ul>
<pre><code class='language-pseudocode' lang='pseudocode'>^[a-z][1-9][^a-z][^A-Z][A-Z]
</code></pre>
<p>&nbsp;</p>
