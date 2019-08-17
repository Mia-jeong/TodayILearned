<h1><a name="header-n158" class="md-header-anchor md-print-anchor" href="af://n158"> </a><span>네트워크 계층의 역할 및 IP개념</span></h1>
<h5><a name="header-n159" class="md-header-anchor md-print-anchor" href="af://n159"> </a><span>1. 네트워크 계층의 역할</span></h5>
<ul>
<li><span>네트워크 계층은 </span><code>서로 다른 네트워크</code><span>에 있는 목적지로 데이터를 전송하기 위해 필요한 계층이다.</span></li>

</ul>
<ul>
<li><span>데이터 링크계층에서는 </span><code>같은 네트워크</code><span>에 있는 컴퓨터로는 데이터 전송이 가능하지만 다른 네트워크로는 전송이 불가능</span></li>

</ul>
<h5><a name="header-n166" class="md-header-anchor md-print-anchor" href="af://n166"> </a><span>2. 라우터(Router)</span></h5>
<ul>
<li><span>전송 하려는 데이터의 목적지가 정해지면 목적지까지 어떤 경로로 가면 좋은지 알려주는 역할</span></li>
<li><code>IP 주소</code><span>: 특정 네트워크의 특정 네트워크를 구별 할 수 있는 주소</span></li>
<li><code>라우팅(Routing)</code><span>: 특정 IP 주소까지 데이터를 보낼 경로를 결정하는 것</span></li>
<li><code>레이어 3 스위치</code><span>: 네트워크를 분할하여 라우팅을 할 수 있는 네트워크 장비</span></li>
<li><code>라우팅 테이블(Routing Table)</code><span>: 라우팅 경로를 등록, 저장, 관리</span></li>
<li><code>IP 패킷</code><span>: IP프로토콜을 사용하여 전송 정보(</span><code>출발지 IP주소</code><span>, </span><code>도착지 IP주소</code><span> 등)등을 헤더에 담아 캡슐화 한 정보</span></li>

</ul>
<h5><a name="header-n180" class="md-header-anchor md-print-anchor" href="af://n180"> </a><span>3. IP </span></h5>
<ul>
<li><p><span>특정 네트워크의 특정 네트워크를 구별 할 수 있는 주소</span></p>
</li>
<li><p><code>인터넷 서비스 제공자(ISP)</code><span> 를 통해 부여 된다.</span></p>
</li>
<li><p><span>IP 버전</span></p>
<ul>
<li><code>IPv4</code><span>: 32비트로 구성 되어 있으며 IP주소를 43억개 생성 할 수 있음</span></li>
<li><code>IPv6</code><span>: 인터넷이 보급되면서 더 많은 IP주소가 필요하게 되어 생성 128비트로 되어있으며 거의 무한대의 아이피 주소를 생성할 수 있음</span></li>

</ul>
</li>
<li><p><span>IP 주소</span></p>
<ul>
<li><p><code>공인 IP</code><span>:ISP 에게서 제공받은 IP주소로 인터넷이 직접적으로 연결되는 컴퓨터나 라우터에 공인 IP주소를 할당</span></p>
</li>
<li><p><code>사설 IP</code><span>: 회사나 가정의 랜에 있는 컴퓨터는 사설IP주소를 할당 받아 사용</span></p>
<p>											<code>인터넷</code></p>
<p><span>                                </span>				<span>| (공인IP) </span></p>
<p>											<code>공유기</code></p>
<p>												<span>| (사설 IP)</span></p>
<p>				<code>컴퓨터</code><span>(사설IP), </span><code>컴퓨터</code><span>(사설IP), </span><code>컴퓨터</code><span>(사설IP)</span></p>
</li>
<li><p><code>공유기</code><span> 는 사설 IP들이 인터넷에 접속할 때 공인 IP를 달고 외부에 나가고 들어올 수 있도록 IP 변환 작업을 해준다. 따라서 외부에서 볼땐 공인 IP하고만 통신하는 것처럼 보임</span></p>
</li>
<li><p><span>주로, 공인 IP주소는 라우터에만 할당 하고 랜안에 있는 컴퓨터에는 랜의 네트워크 관리자가 자유롭게 사설 IP주소를 할당하거나 라우터의 DHCP기능을 사용하여 주소를 자동으로 할당</span></p>
</li>
<li><p><code>MAC</code><span> 주소는 48비트로 구분하기 쉽도록 16진수로 표현</span></p>
</li>
<li><p><code>IP</code><span> 주소는 32비트로 구분하기 쉽도록 10진수로 표시, (실제 IP주소는 2진수로 표현)</span></p>
</li>
<li><p><code>네트워크 ID</code><span>: 어떤 네트워크인지 구별하는 ID</span></p>
</li>
<li><p><code>호스트 ID</code><span>: 특정 네트워크의 어떤 컴퓨터인지 나타내는 ID</span></p>
</li>

</ul>
</li>

</ul>
