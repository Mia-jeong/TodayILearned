<h1><a name="header-n101" class="md-header-anchor md-print-anchor" href="af://n101"> </a><span>비트연산자</span></h1>
<p>&nbsp;</p>
<h3><a name="header-n103" class="md-header-anchor md-print-anchor" href="af://n103"> </a><span>1. 비트연산자</span></h3>
<p><code>비트</code><span> 란 자료를 표현 하는 최소 단위로 0, 1로 표현 된다. 비트 연산자란 이러한 비트들을 서로 연산 할 수 있도록 계산해주는 연산자이다.</span></p>
<h3><a name="header-n105" class="md-header-anchor md-print-anchor" href="af://n105"> </a><span>2. 비트연산자의 장점</span></h3>
<p><span>bit연산의 장점은 바로 </span><code>스피드</code><span> 이다. bit 는 다른 추상화된 정보들과 달리 </span><code>재현</code><span> 의 과정을 거치지 않고 즉시 해석 되엇 의미를 전달 하기 때문에 그만 큼 빠르다.</span></p>
<p><span>즉, </span><code>3 * 2</code><span> 보다 </span><code>3 &lt;&lt; 1</code><span> 이 속도 면에서 더 빠르다. </span></p>
<h3><a name="header-n108" class="md-header-anchor md-print-anchor" href="af://n108"> </a><span>3. 비트연산자의 종류</span></h3>
<figure><table>
<thead>
<tr><th><span>Category</span></th><th><span>Description</span></th></tr></thead>
<tbody><tr><td><span>&amp;</span></td><td><span>연산 하는 두 비트가 모두 1일 경우 1, 하나라도 0이라면 0</span></td></tr><tr><td><span>|</span></td><td><span>연산 하는 두 비트중 하나라도 1이라면 1, 둘 다 0이라면 0</span></td></tr><tr><td><span>^</span></td><td><span>연산 하는 두 비트 가 서로 다를 경우 1, 즉 1, 0 혹은 0, 1 일 경우에만 1</span></td></tr><tr><td><span>&lt;&lt;</span></td><td><span>비트를 왼쪽으로 shift, 빈 자리는 0으로 채워진다. </span><br><span>9 &lt;&lt; 2  는 9 </span><code>곱하기</code><span> 2^2 를 한 것과 같다.</span></td></tr><tr><td><span>&gt;&gt;</span></td><td><span>비트를 오른쪽으로 shift, 빈 자리는 최상위의 부호 비트와 같은 값으로 채워진다.</span><br><span>9 &gt;&gt;2 는 9 </span><code>나누기</code><span> 2^2를 한 것과 같다.</span></td></tr><tr><td><span>&gt;&gt;&gt;</span></td><td><span>비트를 오른쪽 으로 이동, 이동 하면서 빈 부분은 0으로 채워줌</span><br><span>0010 0000 &gt;&gt;&gt; 2</span><br><span>0000 1000</span></td></tr><tr><td><span>~</span></td><td><span>비트를 반전 시킨다 </span><br><span>~0100 1101</span><br><span>  1011 0010</span></td></tr></tbody>
</table></figure>
<h3><a name="header-n134" class="md-header-anchor md-print-anchor" href="af://n134"> </a><span>4. 실습</span></h3>
<pre><code class='language-java' lang='java'>public class Main {

    public static void main(String[] args) {
        int a = 0B00010001; //17
        int b = 0B01000011; //67

        System.out.println(a & b); // 1
        System.out.println(a | b); // 83
        System.out.println(a ^ b); // 82
        System.out.println(b << 1); //134
        System.out.println(b >> 2); //16
        System.out.println(b <<< 2); //16
        System.out.println(~b); //~68
    }
}
</code></pre>
<p>&nbsp;</p>
