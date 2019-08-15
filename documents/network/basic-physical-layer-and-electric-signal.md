<h1><a name="header-n210" class="md-header-anchor md-print-anchor" href="af://n210"> </a><span>네트워크 물리계층이 하는 일 과 전기신호</span></h1>
<h5><a name="header-n211" class="md-header-anchor md-print-anchor" href="af://n211"> </a><span>1 물리계층</span></h5>
<ul>
<li><span>물리계층은 0, 1 비트열(데이터)를 전기 신호로 변환하는 역할을 한다.</span></li>

</ul>
<h5><a name="header-n215" class="md-header-anchor md-print-anchor" href="af://n215"> </a><span>2. 전기신호</span></h5>
<ul>
<li><p><span>데이터는 전기신호로 변환되어 네트 워크로 전송 된다.</span></p>
<p><code>컴퓨터</code><span>  &gt; </span><code>0,1</code><span> &gt; </span><code>전기신호</code><span> &gt; </span><code>0.1</code><span> &gt; </span><code>컴퓨터</code></p>
</li>
<li><p><span>전기 신호의 종류</span></p>
<ul>
<li><span>아날로그 신호 : 전기신호가 물결모양으로 생겼다. 전화 회선, 라디오 방송에 사용 된다.</span></li>
<li><span>디지털 신호: 전기 신호가 직각으로 생겼다.</span></li>
<li><span>컴퓨터의 </span><code>메인 보드</code><span> 에 </span><code>내장형 랜카드</code><span> 를 가지고 있는데 이러한 </span><code>랜 카드</code><span> 가 데이터를 전기신호로 변환 시킨다.</span></li>

</ul>
</li>

</ul>
<h5><a name="header-n229" class="md-header-anchor md-print-anchor" href="af://n229"> </a><span>3. 케이블의 종류</span></h5>
<ul>
<li><p><span>케이블은 데이터를 전송하기 위한 </span><code>전송매체</code><span> 이다. </span><code>전송매체</code><span> 란 데이터가 흐르는 물리적인 선로를 의미한다.</span></p>
</li>
<li><p><span>케이블 종류에는 유선 과 무선이 존재한다.</span></p>
</li>
<li><p><span>유선: 직접 케이블로 서로 연결되어있는 연결 되어 데이터를 주고 받는 것을 의미한다.</span></p>
<ul>
<li><span>트위스트 페어 케이블 : 꼬임선, 이중 나선 케이블로 UTP 와 STP 두가지 종류가 존재한다.</span></li>
<li><span>광케이블 : 데이터 전송을 위해 광섬유로 만든 케이블, 레이저를 이용해서 통신 하기 때문에 구리선과는 비교 할 수 없을 만큼의 장거리 &amp; 고속통신이 가능</span></li>

</ul>
</li>
<li><p><span>무선: 직접 케이블로 서로 연결되어 있는 것이 아닌 말 그대로 무선으로 데이터를 주고 받는 것을 의미</span></p>
<p><span>한다.</span></p>
<ul>
<li><span>라디오 파: 가장 긴 파장을 가진 전자기파, 파장이 몇 m에서 수천 Km에 이르는 전자기파로 주파수는 수백 Hz에서 몇 수백만 Hz에 해당</span></li>
<li><span>마이크로파: 마이크로파는 라디오파와 적외선 사이의 파장과 주파수를 가지고 있는 전자기파. 보통 파장이 1mm와 1dm사이의 전자기 방사이다.</span></li>
<li><span>적외선 : 가시광선 보다  파장이 길고 전자레인지에  사용하는 마이크로파보다 파장이 짧다. 일상적으로 어둠 속에서 열을 내는 물체를 가까이 하면 피부로 온도를 느낄 수 있는데 이것이 적외선</span></li>

</ul>
</li>

</ul>
<h5><a name="header-n252" class="md-header-anchor md-print-anchor" href="af://n252"> </a><span>4. 트위스트 페어 케이블 (랜케이블)</span></h5>
<p><span>트위스트 페어 케이블에 대해 좀더 자세히 알아보자. 트위스트 페어 케이블은 가장 많이 사용되는 유선 케이블이며 </span><code>랜케이블</code><span> 이라고도 불린다.</span></p>
<figure><table>
<thead>
<tr><th><span>Category</span></th><th><span>Description</span></th><th><span>Shield</span></th><th><span>Price</span></th><th><span>Noise</span></th></tr></thead>
<tbody><tr><td><span>UTP(Unshielded Twisted Pair)</span></td><td><span>비차폐 연선으로 구리 8개가 서로 꼬여있다. UTP케이블은 전송 품질에 따라 분류가 가능하며 저렴하기 때문에 가장많이 사용 되는 케이블이다.</span></td><td><span>X</span></td><td><span>저렴</span></td><td><span>큼</span></td></tr><tr><td><span>STP(Shileded Twisted Pair)</span></td><td><span>차폐연선으로  두 개씩 꼬아 만 든 선을 실드로 보호한 케이블</span></td><td><span>O</span></td><td><span>비쌈</span></td><td><span>적음</span></td></tr></tbody>
</table></figure>
<ul>
<li><p><code>실드</code><span> : 금속매듭 같은 것으로 외부에서 발생 하는 </span><code>노이즈</code><span> 를 막아주는 역할을 한다.</span></p>
</li>
<li><p><code>노이즈</code><span>: 케이블에 전기 신호가 흐를 때 발생하는 것</span></p>
</li>
<li><p><code>RJ-45/커넥터</code><span>: 케이블 양쪽에 달려 있으며 장비를 연결할때 사용 </span></p>
</li>
<li><p><span>랜케이블의 종류에는 </span><code>다이렉트 케이블</code><span> 과 </span><code>크로스 케이블</code><span> 이 존재한다</span></p>
<ul>
<li><span>다이렉트 케이블: 구리선 8개가 서로 다이렉트(같은 순서)로 연결 되어있으며 컴퓨터 &lt;-&gt; 스위치 간 연결 시 사용 된다.</span></li>
<li><span>크로스 케이블: 구리선 8개가 서로 크로스(같은 순서X) 되어 연결 되어 있으며 컴퓨터 &lt;-&gt; 컴퓨터 간 연결 시 사용 된다.</span></li>

</ul>
</li>

</ul>
<h5><a name="header-n287" class="md-header-anchor md-print-anchor" href="af://n287"> </a><span>5. 리피터와 허브</span></h5>
<p><code>리피터</code><span>와 </span><code>허브</code><span>는 물리계층의 네트워크 장비에 존재 한다.</span></p>
<ul>
<li><p><span> 리피터(Repeater)</span></p>
<ul>
<li><p><span>리피터는 일그러진 전기 신호를 복원 하고 증폭하는 기능 을 가진 네트워크 중계장비이다.</span></p>
</li>
<li><p><span>그렇기 때문에 통신하는 상대방이 멀리 있을때 리피터를 사이에 넣어 상대방과 통신 할 수 있도록 파형을 정상적으로 만드는 역할을 한다.</span></p>
<p><code>컴퓨터</code><span>  ———————</span><code>리피터</code><span>———————</span><code>컴퓨터</code></p>
</li>
<li><p><span>그러나, 요즘은 다른 네크워크 장비가 리피터의 기능을 지원하여 잘 사용하지 않는다.</span></p>
</li>

</ul>
</li>

</ul>
<ul>
<li><p><span>허브(Hub)</span></p>
<ul>
<li><span>일대일 통신만 가능한 리피터와 달리 허브는 여러개의 </span><code>포트</code><span> 를 가지고 있어 여러대의 컴퓨터와 통신이 가능하다.</span></li>
<li><span>사무실이나 가까운 거리에 있는 장비들을 케이블을 사용하여 연결하는 장치</span></li>
<li><span>허브 역시 리피터와 같이 전기 신호를 복원 및 증폭하는 역할을 한다.</span></li>
<li><span>허브는 컴퓨터 여러 대를 서로 연결 하는 장치 역할 을 한다. 따라서 직접 컴퓨터 끼리 연결하지 않아도 통신을 서로 통신이 가능하도록 만든다. 하지만 1대의 컴퓨터가 포트로 데이터를 전송하면 나머지 모든 컴퓨터에게 해당 데이터가 전송 된다는 단점이 있다. 이러한 단점을 보완 하기 위하여 </span><code>스위치</code><span> 가 탄생 하였다.</span></li>

</ul>
</li>

</ul>
<p><span> </span></p>
