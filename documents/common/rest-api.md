<h1><a name="header-n115" class="md-header-anchor md-print-anchor" href="af://n115"> </a><span>REST API</span></h1>
<h3><a name="header-n116" class="md-header-anchor md-print-anchor" href="af://n116"> </a><span>Rest API(Representational State Transfer) 란?</span></h3>
<p><span>REST API 란 표현상태를 전달 하는 것을 의미한다. 즉 Resource를 처리하는 것을 의미한다.</span></p>
<p><span>Resource처리에는 다음과 같이 4가지 기능이 있다.</span></p>
<p>&nbsp;</p>
<figure><table>
<thead>
<tr><th><span>Create</span></th><th><span>Read</span></th><th><span>Update</span></th><th><span>Delete</span></th></tr></thead>
<tbody><tr><td><span>POST</span></td><td><span>GET</span></td><td><span>PUT/PATCH</span></td><td><span>DELETE</span></td></tr></tbody>
</table></figure>
<h3><a name="header-n131" class="md-header-anchor md-print-anchor" href="af://n131"> </a><span>URI AND URL</span></h3>
<p><span>리소스를 지정할때 우리는 URI(Uniform Resource Identifier)을 사용하기도 하고 URL(Uniform Resource Locator)을 사용하기도 한다. 특히 URL은 우리가 웹서핑을 할때 많이 사용되는 방식이다.</span></p>
<p><span>URL은 URI에 포함된다 따라서 URI가 상위 개념이고 URL은 URI에 속하는 하위 개념이다. 그렇다면 URI와 URL은 무엇일까?</span>
<span>URL은 말그대로 우리가 찾고 자 하는 자원이 어디에 있는지 알려주는 것이다.</span></p>
<p><span> </span><a href='http://helloworld.com/index.html' target='_blank' class='url'>http://helloworld.com/index.html</a><span>  &lt; 바로 옆의 주소를 살펴보자 (가짜 주소임) 우리는 helloworld.com이라는 사이트에서 index.html파일을 찾는것이다. 따라서 해당주소는 URL이다.</span></p>
<p><span>URL는 다음과 같다.</span></p>
<p><span> </span><a href='https://helloworld.com/gretting?name=mia' target='_blank' class='url'>https://helloworld.com/gretting?name=mia</a><span> &lt; 다음 사이트를 열면 name옆의 값에 따라 해당 이름을 가진 사람한테 인사를 하는 내용이 나온다고 가정하자(가짜 주소임 클릭하지 마세요.) 여기서 name의 value값이 무엇이냐에 따라 인사를 받는 사람은 달라 질것이다. 여기에서 주소는 </span><a href='https://helloworld.com/gretting' target='_blank' class='url'>https://helloworld.com/gretting</a><span> 까지고 정보를 얻기 위해서는 name=mia라는 식별자가 필요하기 때문에 해당 주소는 URI이다.</span></p>
<h3><a name="header-n137" class="md-header-anchor md-print-anchor" href="af://n137"> </a><span>Collection And Member</span></h3>
<p><span>리소스는 크게 두가지로 분류할 수 있는 데 하나는 Collection 이고 다른 하나는 Member(그 안에 속한 개별적인 리소스)이다.</span></p>
<figure><table>
<thead>
<tr><th><span>Collection</span></th><th><span>Member</span></th></tr></thead>
<tbody><tr><td><span>Read(List), Create</span><br><span>읽기와 생성이 가능</span></td><td><span>Read(Detail), Update, Delete</span><br></td></tr><tr><td><a href='http://localhost:8080/restaurants' target='_blank' class='url'>http://localhost:8080/restaurants</a></td><td><a href='http://host/restaurants/1/' target='_blank' class='url'>http://host/restaurants/1/</a><span>{id}</span></td></tr></tbody>
</table></figure>
<p>&nbsp;</p>
<blockquote><p><span>가게 목록을 얻고 싶은 경우</span></p>
</blockquote>
<h5><a name="header-n152" class="md-header-anchor md-print-anchor" href="af://n152"> </a><span>GET /restaurants</span></h5>
<blockquote><p><span>가게 상세 정보를 얻고 싶은 경우</span></p>
</blockquote>
<h5><a name="header-n155" class="md-header-anchor md-print-anchor" href="af://n155"> </a><span>GET /restaurants/1</span></h5>
<blockquote><p><span>가게를 추가하고 싶은 경우</span></p>
</blockquote>
<h5><a name="header-n158" class="md-header-anchor md-print-anchor" href="af://n158"> </a><span>POST /restaurants</span></h5>
<blockquote><p><span>가게의 정보를 수정 하는 경우</span></p>
</blockquote>
<h5><a name="header-n161" class="md-header-anchor md-print-anchor" href="af://n161"> </a><span>PATCH /restaurants/1</span></h5>
<blockquote><p><span>가게의 정보를 삭제 하는 경우</span></p>
</blockquote>
<h5><a name="header-n164" class="md-header-anchor md-print-anchor" href="af://n164"> </a><span>DELETE /restaurants/1</span></h5>
<p>&nbsp;</p>
