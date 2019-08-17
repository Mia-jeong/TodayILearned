<h1><a name="header-n187" class="md-header-anchor md-print-anchor" href="af://n187"> </a><span>통신의 종류</span></h1>
<h5><a name="header-n188" class="md-header-anchor md-print-anchor" href="af://n188"> </a><span>1. 단반향 통신(Simplex transmisson) </span></h5>
<ul>
<li><span>데이터의 흐름이 한 방향으로만 한정되어 있는 통신 방식, 일방적인 송식 혹은 수신만이 가능</span></li>
<li><span>텔레비전 방송, 라디오</span></li>

</ul>
<h5><a name="header-n194" class="md-header-anchor md-print-anchor" href="af://n194"> </a><span>2. 반 이중 통신(Half duplex transmisson)</span></h5>
<ul>
<li><span>회선 하나로 송신과 수신을 번갈아 가면서 하는 통신 방식</span></li>
<li><span>주 컴퓨터와 단말기가 반이중 통신을 할 경우, 주 컴퓨터가 단말기에 데이터를 보내는 동안은 단말기에서 데이터를 입력할 수 없으며, 반대로 단말기에서 데이터가 입력되고 있는 동안은 주 컴퓨터가 단말기로 데이터를 보낼 수 없다.</span></li>
<li><span>휴대용 무선 통신기, 인터넷 폰, 허브를 사용한 연결</span></li>

</ul>
<h5><a name="header-n202" class="md-header-anchor md-print-anchor" href="af://n202"> </a><span>3. 전 이중 통신(Full duplex transmisson)</span></h5>
<ul>
<li><span>데이터 송수신을 동시에 하는 통신 방식</span></li>
<li><span>동시에 양방향 전송을 하려면 송신용과 수신용의 2쌍의 전송로가 각각 필요하므로 4선식 전송로로 구성</span></li>
<li><span>컴퓨터간 직접 랜 케이블(크로스 케이블)로 연결 하는 방식, 스위치를 사용한 연결</span></li>

</ul>
<h5><a name="header-n210" class="md-header-anchor md-print-anchor" href="af://n210"> </a><span>4. 충돌 도메인(collision domain)</span></h5>
<ul>
<li><span>반 이중 통신 방식으로 동시에 데이터를 전송할 경우 충동일 일어 난다. 충돌이 발생할 때 그 영향이 미치는 범위를 </span><code>충돌 도메인</code><span> 이라고 한다.</span></li>
<li><span>허브에서는 연결된 모든 컴퓨터가 충돌 도메인이 된다(데이터를 전송시 나머지 컴퓨터에도 데이터가 전달되는 방식이므로)</span></li>
<li><span>네트워크를 지연시키지 않기 위해서 충돌 도메인의 </span><code>범위</code><span> 를 좁히는 것이 매우 중요</span></li>

</ul>
<h5><a name="header-n218" class="md-header-anchor md-print-anchor" href="af://n218"> </a><span>5. ARP(Address Resolution Protocol)</span></h5>
<ul>
<li><span>목적지의 컴퓨터의 </span><code>IP</code><span> 주소를 이용하여 </span><code>MAC</code><span> 주소를 찾기 위한 프로토콜</span></li>
<li><code>ARP 요청</code><span>: 목적지의 MAC주소를 알아내기 위해 네트워크에 브로드 캐스트</span></li>
<li><code>ARP 응답</code><span>: ARP요청을 했을경우 지정된 IP주소를 가지고 있는 컴퓨터가 MAC주소를 응답하는 것</span></li>
<li><code>ARP 테이블</code><span>: ARP 요청과 ARP응답후 얻은 MAC주소와 IP의 매핑 정보를 메모리에 보관</span></li>
<li><span>IP가 변경되면 MAC 주소도 변경 되기 때문에 통신이 불가능 하다, 따라서 ARP 테이블은 보존기간을 ARP캐시로 정 한 후 일정시간이 지나면 삭제 후 ARP를 재요청</span></li>

</ul>
<ul>
<li><code>arp -a</code><span> : ARP 캐시확인</span></li>
<li><code>arp -d</code><span>: ARP 캐시 강제 삭제</span></li>

</ul>
<p>&nbsp;</p>
<h5><a name="header-n236" class="md-header-anchor md-print-anchor" href="af://n236"> </a><span>6. 이더넷은 종류</span></h5>
<p><span>이더넷은 케이블 종류나 통신속도에 따라 다양한 규격으로 분류 된다.규격이름의 정보는 다음과 같이 구별 할 수 있다.</span></p>
<p><code>10</code><span> </span><code>BASE</code><span> </span><code>T</code></p>
<p><code>10</code><span>: 통신속도</span></p>
<p><code>BASE</code><span>: 통신방법(BASEBAND)</span></p>
<p><code>T</code><span>: 테이블 </span></p>
<p><span>종류 : </span><code>10BASE5</code><span>, </span><code>10BASE2</code><span>, </span><code>10BASE-T</code><span>, </span><code>100BASE-TX</code><span>, </span><code>1000BASE-T</code><span>, </span><code>10GBASE-T</code><span> ...</span></p>
<p>&nbsp;</p>
