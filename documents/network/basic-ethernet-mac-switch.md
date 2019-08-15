<h1><a name="header-n178" class="md-header-anchor md-print-anchor" href="af://n178"> </a><span>데이터 링크 계층(이더넷/MAC), 스위치</span></h1>
<h5><a name="header-n179" class="md-header-anchor md-print-anchor" href="af://n179"> </a><span>1. 데이터 링크 계층</span></h5>
<ul>
<li><span>랜에서 데이터를 주고 받기 위해서는 데이터링크 계층의 기술이 필요하다. </span></li>

</ul>
<ul>
<li><span>데이터 링크계층은 네트워크 장비간 신호를 주고 받는 규칙을 정한다.</span></li>

</ul>
<h5><a name="header-n186" class="md-header-anchor md-print-anchor" href="af://n186"> </a><span>2. 이더넷(Ethernet)</span></h5>
<p><span>이더넷은 네트워크 장비간 시호를 주고 받는 규칙중 가장 많이 사용 되는 규칙이다.</span></p>
<ul>
<li><p><span>허브에서 한 컴퓨터가 특정 컴퓨터로만 데이터를 수신, 송신 하고 싶은 경우 데이터에 목적지 정보를 추가해서 보내고 그 이외의 컴퓨터는 데이터를 수신 받아도 무시해버리는 것이 규칙</span></p>
</li>
<li><p><span>또한 동시에 여러대의 컴퓨터가 데이터를 전송 하면 충돌이 일어날 수 있는데 이더넷은 이러한 충돌이 이일어나지 않는 구조로 되어 있다. 충돌을 방지하기 위해 이더넷은 데이터 전송의 시점을 늦추는 데 이를 CSMA/CD라고 한다.</span></p>
<ul>
<li><code>CS</code><span>: 데이터를 송신하는 컴퓨터가 수신하는 컴퓨터 케이블에 신호가 흐르는지 체크</span></li>
<li><code>MA</code><span>: 케이블 신호가 흐르지 않다면 데이터를 수신가능</span></li>
<li><code>CD</code><span>: 충돌이 발생하고 있는지 확인</span></li>

</ul>
</li>
<li><p><span>요즘에는 CSMA/CD보다 </span><code>스위치</code><span> 를 사용한다.</span></p>
</li>

</ul>
<p>&nbsp;</p>
<h5><a name="header-n203" class="md-header-anchor md-print-anchor" href="af://n203"> </a><span>3. MAC(Media Access Control Address) 주소</span></h5>
<p><span>랜카드에는 제조 할때 새겨지는 물리 주소 인 </span><code>MAC 주소</code><span> 가 정해져 있는데 전 세계에 각각 하나씩만 존재하는 유일 한 번호이다. 컴퓨터는 이러한 MAC주소를 통해 서로의 송신지와 수신지를 파악 하여 네트워크로 데이터를 송수신 할 수 있다.</span></p>
<ul>
<li><p><span> 데이터링크 계층에서는 전송되는 데이터에 </span><code>이더넷 헤더</code><span> 와 </span><code>트레일러</code><span> 를 붙인다. </span></p>
</li>
<li><p><code>헤더</code><span> 에는 다음과 같은 정보가 들어간다.</span></p>
<ul>
<li><code>목적지 MAC 주소</code><span> : 6바이트</span></li>
<li><code>출발지 MAC 주소</code><span> : 6바이트</span></li>
<li><code>데이터 유형</code><span> : 2바이트 (이더넷으로 전송 되는 상위계층 프로토콜 종류)</span></li>

</ul>
</li>

</ul>
<ul>
<li><code>트레일러(FCS: Frame Check Sequence)</code><span>: 데이터 전송시 오류가 발생하는 지 확인 하는 용도</span></li>
<li><code>프레임</code><span>: 헤더와 트레일러가 추가된 데이터</span></li>

</ul>
<h5><a name="header-n222" class="md-header-anchor md-print-anchor" href="af://n222"> </a><span>4. 스위치 (Switch)</span></h5>
<ul>
<li><p><span>허브와 달리 데이터 충돌이 일어나지 않음</span></p>
</li>
<li><p><span>데이터링크 계층에서 동작</span></p>
</li>
<li><p><span>내부에 </span><code>Mac Address Table</code><span> 이 존재 </span></p>
<ul>
<li><code>Mac Address Table</code><span>: 스위치의 포트번호와 해당 포트에 연결되어 있는 컴퓨터의 MAC주소가 등록되어 있는 데이터베이스</span></li>
<li><code>Mac 주소 학습</code><span>: 데이터 전송시 Mac Address Table에 수신지 Mac Address가 등록되어 있지 않으면 Mac Address를 포트와 함께 등록</span></li>
<li><code>Flooding</code><span>: 한 컴퓨터에서 데이터 전송 시 수신지의 Mac Address가 아직 Mac Table에 저장되어 있지 않은 경우 다른 컴퓨터로 데이터를 전송</span></li>
<li><code>Mac Address Filtering</code><span>: 데이터 전송 시 등록된 Mac Address 기준으로 데이터를 선별하여 전송하는 기능</span></li>

</ul>
</li>

</ul>
