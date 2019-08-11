<h1><a name="header-n661" class="md-header-anchor md-print-anchor" href="af://n661"> </a><span>[BASIC]네트워크의 의미와 통신규약 기본개념</span></h1>
<h5><a name="header-n662" class="md-header-anchor md-print-anchor" href="af://n662"> </a><span>1. 네트워크</span></h5>
<p><span>네트워크란 컴퓨터와 컴퓨터끼리의 통신을 의미한다.</span></p>
<h5><a name="header-n664" class="md-header-anchor md-print-anchor" href="af://n664"> </a><span>2. 인터넷 </span></h5>
<p><span>인터넷이란 거대한 네트워크를 의미한다.</span></p>
<h5><a name="header-n666" class="md-header-anchor md-print-anchor" href="af://n666"> </a><span>3. 패킷</span></h5>
<p><span>패킷이란 컴퓨터끼리 서로 데이터를 전송할때 사용하는 작은 전송단위를 의미한다.</span></p>
<p><span>컴퓨터끼리 서로 데이터를 전송할때 왜 작은단위로 쪼개서 전송하는 것일까? 전송의 대역폭은 한정적이여서 큰단위의 데이터가 들어온다면 그로 인하여 지체현상이 발생할것이다. 그렇기 때문에 통신을 원활하게 하기위하여 데이터를 작은 단위로 쪼개어 전송하여야 한다.</span></p>
<h5><a name="header-n669" class="md-header-anchor md-print-anchor" href="af://n669"> </a><span>4. 정보의 단위</span></h5>
<p><span>컴퓨터는 0과 1만을 이해한다.</span></p>
<figure><table>
<thead>
<tr><th><span>Category</span></th><th><span>Size</span></th><th><span>Description</span></th></tr></thead>
<tbody><tr><td><span>1bit</span></td><td><span>1bit</span></td><td><span>2진수의 표현으로 0, 1의 두가지 정보를 나타낸다</span></td></tr><tr><td><span>1byte</span></td><td><span>8bit</span></td><td><span>기억단위의 기본이데는 단위로 8비트로 구성된다.</span></td></tr><tr><td><span>1word</span></td><td><span>2byte</span></td><td><span>컴퓨터에서 연산의 기본단위가 되는 정보의 양을 의미한다.</span></td></tr><tr><td><span>Ascii</span></td><td>&nbsp;</td><td><span>우리가 사용하는 문자들을 표현하기 위한 문자표이며 256개이다. 모든 문자에 0~255의 값을 부여하여 1바이트를 사용하여 모두 표현할 수 있도록 각 문자에 값을 매칭 시킨다.( 우리가 컴퓨터에서 문자를 사용할 수 있는 이유는 이러한 Ascii코드 덕분이다.)</span></td></tr></tbody>
</table></figure>
<h5><a name="header-n692" class="md-header-anchor md-print-anchor" href="af://n692"> </a><span>5. LAN과 WAN</span></h5>
<figure><table>
<thead>
<tr><th><span>Category</span></th><th><span>Description</span></th></tr></thead>
<tbody><tr><td><span>LAN(Local Area Network)</span></td><td><span>근거리 통신망을 의미한다.</span><br><span>- 범위: 좁음</span><br><span>- 속도: 빠름</span><br><span>- 오류: 적음</span></td></tr><tr><td><span>WAN(Wide Area Network)</span></td><td><span>장거리 통신망을 의미한다.(인터넷)</span><br><span>- 범위: 넓음</span><br><span>- 속도: 빠름</span><br><span>- 오류: LAN에 비해 많음</span></td></tr></tbody>
</table></figure>
<ul>
<li><p><span>가정용 LAN구성 방법 </span></p>
<ul>
<li><span>ISP와 인터넷 회선결정</span></li>
<li><span>ISP와 인터넷 공유기 필요 </span></li>
<li><span>유선: 랜케이플 연결 O</span></li>
<li><span>무선: 랜케이블 연결 X</span></li>

</ul>
</li>
<li><p><span>회사네트워크 구성</span></p>
<ul>
<li><span>회사네트워크를 구성하기 위해서는 DMZ가 필요하다.</span></li>
<li><span>DMZ (Demiliterized Zone):  외부로 공개하기 위한 서버</span></li>
<li><span>DMZ에는주로 웹서버, 메일서버, DNS가 있다. </span></li>
<li><span>회사서버는 주로 OnPremise(데이터 센터이용, 클라우드 시스템이용) 나 클라우드를 사용하여 구축한다.</span></li>
<li><span>회사내의 컴퓨터나 프린트는 스위치나 무선LAN을 사용하여 접속한다.</span></li>

</ul>
</li>

</ul>
<h5><a name="header-n728" class="md-header-anchor md-print-anchor" href="af://n728"> </a><span>5. 통신규약</span></h5>
<ul>
<li><code>Protocol</code><span>:컴퓨터 간에 데이터를 주고받을 시 통신 하는 방법에 대한 규칙 및 표준 </span></li>

</ul>
<ul>
<li><p><code>OSI</code><span>: ISO에서 제정한 모델로 네트워크에서 데이터를 주고 받기 위한 통신규약을 의미한다. 즉, 컴퓨터간에 데이터를 전달 하기 위해서 컴퓨터 내부에서 해당 규약에 따라 여러 가지일을 하는 것을 의미한다.</span></p>
<figure><table>
<thead>
<tr><th><span>No.</span></th><th><span>Category</span></th><th><span>Description</span></th></tr></thead>
<tbody><tr><td><span>7계층</span></td><td><span>응용계층(Application)</span></td><td><span>최종 사용자에게 가장 가까운 계층으로 해당 계층에서 작동하는 응용프로그램은 사용자와 직접적으로 상호작용을 한다 Ex)구글 크롬, 파이어폭스, 사파리등 웹브라우저, 스카이프,아웃룩,오피스 프로그램</span></td></tr><tr><td><span>6계층</span></td><td><span>표현계층(Presentation)</span></td><td><span>응용계층의 데이터표현에서 독립적인 부분을 나타낸다. 응용프로그램이나 네트워크를 위해 데이터를 표현(응용프로그램 형식을 준비, 네트워크 형식 변환 or 네트워크형식 을 응용프로그램 형식으로 변환) 대표적인 예로서는 데이터를 안전하게 전송하기 위해 암호와, 복호화를 하는 계층이다.</span></td></tr><tr><td><span>5계층</span></td><td><span>세션계층(Session)</span></td><td><span>컴퓨터 간, 혹은 서버간 대화를 하기위해서는 세션(session)이 필요하다. 그러한 작업은 다음과 같이 세션계층에서 담당하다. 해당 계층에서는 설정, 조율(ex.시스템응답대기기간), 세션 마지막에 응용프로그램 간 종료등의 기능이 필요하다.</span></td></tr><tr><td><span>4계층</span></td><td><span>전송계층(Transport)</span></td><td><span>해당 계층은 최종 시스템 및 호스트 간의 데이터 전송 조율을 담당한다. 따라서 보낼데이터의 용량, 속도, 목적지등을 처리한다. 전송계층에서 가장 잘 알려진 것이 TCP(전송 제어 프로토콜)이다. TCP는 인터넷 프로토콜(IP)위에 구축되는데 흔히 TCP/IP로 알려져있다. 기기의 IP주소가 전송계층에서 작동한다.</span></td></tr><tr><td><span>3계층</span></td><td><span>네트워크 계층(Network)</span></td><td><span>해당 계층에서는 라우터 의 대부분 기능이 자리잡는다. 즉, 다른 여러 라우터를통한 라우팅을 비롯한 패킷 전달을 담당한다.</span></td></tr><tr><td><span>2계층</span></td><td><span>데이터 링크 계층(Data Link)</span></td><td><span>데이터 링크계층은 노드 간 데이터 전송을 제공하며 물리 계층의 오류 수정도 처리한다. 해당 계층에는 매체 접근 제어(MAC) 계층 과 논리적 연결 제어(LLC)계층등 두 개의 부계층이 존재한다. 대부분 스위치는 이러한 데이터 링크 계층에서 작동한다.</span></td></tr><tr><td><span>1계층</span></td><td><span>물리계층(Physical)</span></td><td><span>물리계층에서는 시스템의 전기적, 물리적 표현을 나타낸다.케이블의 종류, 무선 주파수 링크는 물론 핀 배치, 전압, 물리요건 등이 포함된다. 네트워킹 문제가 발생하면 많은 네트워크 전문가가 물리계층으로 가서 케이블 연결이 제대로 되어있는지, 라우터나 스위치 또는 컴퓨터에서 전원 플러그가 빠지지 않았는지 확인한다.</span></td></tr></tbody>
</table></figure>
<blockquote><p><span>참고 : </span><a href='http://www.ciokorea.com/insider/36536'><span>네트워크의 기본 ‘OSI 7계층’ 한번에 이해하고 외우는 방법</span></a></p>
</blockquote>
</li>

</ul>
<ul>
<li><p><code>TCP/IP</code><span> : 통신규약 중 하나로 가장 많이 쓰이는 프로토콜 이다.</span></p>
<ul>
<li><span>데이터를 안정적으로 전송하고, 속도가 빠르며 독립성이 존재한다</span></li>
<li><span>독립성이란 하드웨어, 운영체제, 접속매체와 관계없이 동작할 수 있는 것을 의미한다.</span></li>

</ul>
<figure><table>
<thead>
<tr><th style='text-align:left;' ><span>Category</span></th><th><span>UsageBy</span></th><th><span>Description</span></th></tr></thead>
<tbody><tr><td style='text-align:left;' ><span>응용계층(Application)</span></td><td><span>User</span></td><td><span>FTP,HTTP등 응용프램에서의 프로토콜이 정의되는 계층으로 웹서비스들을 사람들에게 제공하는 역할을 하며 네트워크를통해 이루고자 하는 작업을 실제로 수행하는 계층</span></td></tr><tr><td style='text-align:left;' ><span>전송계층(Transport)</span></td><td><span>Kernel</span></td><td><span>TCP 와 UDP를 의미하며 어플리케이션과 인터넷 계층 사이의 데이터가 전달 될때 중계역할을 한다.</span></td></tr><tr><td style='text-align:left;' ><span>인터넷계층(Internet)</span></td><td><span>Kernel</span></td><td><span>IP등을 의미하며 패킷이 수신해야 할 상대의 주소를 지정하여 데이터를 전달 </span></td></tr><tr><td style='text-align:left;' ><span>네트워크 접속계층(Network Access)</span></td><td><span>Kernel</span></td><td><span>이더넷, PPP, 와이파이를 의미하여 다른 컴퓨터 등으로 실질적으로 데이터를 전달</span></td></tr><tr><td style='text-align:left;' ><span>물리계층(Physical)</span></td><td><span>Device</span></td><td><span>시스템간의 물리적인 연결과 전기신호 변화 및 제어를 하는 계층</span></td></tr></tbody>
</table></figure>
<blockquote><p><span>참고 : </span><a href='https://jhc9639.blog.me/221411218450'><span>TCP/IP의 이해</span></a></p>
</blockquote>
</li>
<li><p><span>각각의 계층에는 다양한 </span><code>프로토콜(통신규약)</code><span> 이 존재한다.</span></p>
</li>

</ul>
<h5><a name="header-n807" class="md-header-anchor md-print-anchor" href="af://n807"> </a><span>6. 캡슐화와 역캡슐화</span></h5>
<p><span>데이터를 송수신 할 때는 캡슐화와 역캡슐화가 이루어진다.</span></p>
<ul>
<li><span>Header(헤더): 데이터를 전송하기 위해서는 데이터의 앞부분에 전송하는데 필요한 정보를 첨부하여 다음계층으로 보내야 하는데 이를 헤더라고 부른다. 헤더에는 데이터를 전달 받을 상대에 대한 정보도 포함이 되어있다. 이렇게 헤더를 붙여서 데이터를 전송하는 것을 캡슐화 라고 한다.</span></li>

</ul>
<ul>
<li><p><span>캡슐화와 역캡슐화의 흐름</span></p>
<figure><table>
<thead>
<tr><th><span>카테고리</span></th><th><span>데이터 송신</span></th><th><span>캡슐화</span></th><th><span>데이터 수신</span></th><th><span>역캡슐화</span></th></tr></thead>
<tbody><tr><td><span>응용계층</span></td><td><code>데이터</code></td><td><code>1</code></td><td><code>데이터</code></td><td><code>9</code></td></tr><tr><td><span>전송계층</span></td><td><code>헤더</code><span> &gt; </span><code>데이터</code></td><td><code>2</code></td><td><code>헤더</code><span>&lt; </span><code>데이터</code></td><td><code>8</code></td></tr><tr><td><span>네트워크 계층</span></td><td><code>헤더</code><span> &gt; </span><code>헤더</code><span> </span><code>데이터</code></td><td><code>3</code></td><td><code>헤더</code><span> &lt; </span><code>헤더</code><span> </span><code>데이터</code></td><td><code>7</code></td></tr><tr><td><span>데이터 링크 계층</span></td><td><code>헤더</code><span> &gt; </span><code>헤더</code><span> </span><code>헤더</code><span> </span><code>데이터</code><span>&lt; </span><code>트레일러</code></td><td><code>4</code></td><td><code>헤더</code><span> &lt; </span><code>헤더</code><span> </span><code>헤더</code><span> </span><code>데이터</code><span>&gt; </span><code>트레일러</code></td><td><code>6</code></td></tr></tbody>
</table></figure>
<p>							<span>물리 계층</span>					<code>헤더</code><span> </span><code>헤더</code><span> </span><code>헤더</code><span> </span><code>데이터</code><span> </span><code>트레일러</code><span>  </span><code>5</code></p>
<ul>
<li><span>컴퓨터-서버간 통신을 할때 응용계층 에서는 </span><code>1</code><span> 과 같이 요청데이터가 생성된다.</span></li>
<li><span>전송계층 </span><code>2</code><span> 에서는 해당 데이터는 신뢰 할 수 있는 통신이이루어 지기위해 응용계층에서 생성된 헤더를 데이터 에 붙인다. </span></li>
<li><span>네트워크 계층 </span><code>3</code><span> 에서도 네트워크 통신을 위하여 헤더를 데이터에 붙인다. </span></li>
<li><span>마지막 으로 네트워크 계층에서 생성된 데이터에 문리적인 통신채널을 연결하기 위해 </span><code>4</code><span>  데이터 링크 계층에서 헤더와 트레일러를 붙인다.(</span><code>트레일러</code><span> : 데이터를 전달 할때 데이터의 마지막에 추가하는정보 )</span></li>
<li><span>이러한 데이터는 </span><code>전기신호</code><span> 로변환 되어 수신 측에 도착한다.</span></li>
<li><span>역캡슐화에서는 해당 계층을 거꾸로 순회하면서 각각 계층에서 붙였던 헤더 혹은 트레일러를 제거 하며 최종적으로 데이터를 전달 받는다.</span></li>

</ul>
</li>

</ul>
<h5><a name="header-n860" class="md-header-anchor md-print-anchor" href="af://n860"> </a><span>7. VPN(Virtual Private Network) 가상 사설망</span></h5>
<p><span>가상으로 위치를 바꾸어 본래 IP를 숨기고 암호화를 통해 사용자가 온라인에서 무슨 활동을 하는지 알 수 없게 만드는 프로그램. 즉, 공중망을 통한 연결을 전용선 처럼 사용하는 효과를 누리는 것이다. 기업 같은 경우 가상 통신 터널을 만들어 기업 본사나 지사와 같은 거점 간을 연결 하여 통신하거나 외부에서 인터넷으로 사내에 접속 할 경우 이러한 가상통신 터널을 만들어 사용한다. 최근에는 개인이 VPN을 구축하여 사용하는 경우도 많이 있다.</span></p>
