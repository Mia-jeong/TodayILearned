<h1><a class="md-header-anchor md-print-anchor" href="af://n201" name="header-n201"> </a><span>Pivot 실습</span></h1>
<p><span>심심풀이로 종종 HackerRank를 통해 문제를 푸는 중이다. 그러다 오늘 Advanced Select 카테고리에서 Pivot이 필요한 문제를 풀게 되었다 문제는 다음과 같았다.</span></p>
<p>&nbsp;</p>
<p><span>다음과 같은 </span><i><span>Occupation</span></i><span> 테이블이 있다</span></p>
<table>
<thead>
<tr>
<th><span>Name</span></th>
<th><span>Occupation</span></th>
</tr>
</thead>
<tbody>
<tr>
<td><span>Samantha</span></td>
<td><span>Doctor</span></td>
</tr>
<tr>
<td><span>Julia</span></td>
<td><span>Actor</span></td>
</tr>
<tr>
<td><span>Maria</span></td>
<td><span>Actor</span></td>
</tr>
<tr>
<td><span>Meera</span></td>
<td><span>Singer</span></td>
</tr>
<tr>
<td><span>Ashely</span></td>
<td><span>Professor</span></td>
</tr>
<tr>
<td><span>Ketty</span></td>
<td><span>Professor</span></td>
</tr>
<tr>
<td><span>Christeen</span></td>
<td><span>Professor</span></td>
</tr>
<tr>
<td><span>Jane</span></td>
<td><span>Actor</span></td>
</tr>
<tr>
<td><span>Jenny</span></td>
<td><span>Doctor</span></td>
</tr>
<tr>
<td><span>Priya</span></td>
<td><span>Singer</span></td>
</tr>
</tbody>
</table>
<p><span>해당 테이블을 Pivot 하여 아래와 같이 직업에 따라 분류하여 테이블을 출력하라.</span></p>
<table>
<thead>
<tr>
<th><span>Doctor</span></th>
<th><span>Professor</span></th>
<th><span>Singer</span></th>
<th><span>Actor</span></th>
</tr>
</thead>
<tbody>
<tr>
<td><span>Jenny</span></td>
<td><span>Ashley</span></td>
<td><span>Meera</span></td>
<td><span>Jane</span></td>
</tr>
<tr>
<td><span>Samantha</span></td>
<td><span>Christeen</span></td>
<td><span>Priya</span></td>
<td><span>Julia</span></td>
</tr>
<tr>
<td><span>NULL</span></td>
<td><span>Ketty</span></td>
<td><span>NULL</span></td>
<td><span>Maria</span></td>
</tr>
</tbody>
</table>
<p>&nbsp;</p>
<p><span>참고로 HackerRank 문제를 풀때 MySQL을 사용하여 해결한다.</span></p>
<p><span>사실 이전에 Pivot테이블을 작성해 본 적이 없었다 😅 그렇기 때문에 해당 문제를 풀기 위해서 열심히 인터넷에 Pivot 테이블을 사용하는 방법을 구글링 하였다 ㅋㅋ</span></p>
<p>&nbsp;</p>
<p><span>Pivot 테이블을 작성하기 위해서는 다음과 같았다</span></p>
<p>&nbsp;</p>
<blockquote><span>직업이 같은 이름들을 그룹별로 묶어 그룹 내에서 각각 rownum을 부여하자.</span></blockquote>
<p>&nbsp;</p>
<pre class="language-sql"><code>SELECT a.*,
        (CASE @vOccup WHEN a.OCCUPATION THEN @rownum:=@rownum+1 ELSE @rownum:=1 END) rnum,
        (@vOccup:=a.OCCUPATION) vOccup
    FROM OCCUPATIONS a,(SELECT @vOccup:='', @rownum:=0 FROM DUAL) b
    ORDER BY OCCUPATION, NAME 
</code></pre>
<p><span>해당 로직을 작성하기 위해 다음과 같은 쿼리를 작성하였다.</span> <span>a.*밑의 칼럼 로직이 바로 그룹별로 rownum을 설정해주는 로직이다. </span></p>
<p><span>우선, @vOccup(OCCUPATION) 은 바로 전 행까지의 OCCUPATION을 담고 있는 변수를 의미한다. </span></p>
<p><span>이러한 @vOccup이 현재 읽고 있는 행의 a.OCCUPATION과 같다면 (THEN) 전 행까지의 rownum 변수에 rownum+1을 대입해주고 (ELSE) 그렇지 않다면 rownum에 1을 대입해 주는 것이다.</span></p>
<p><span>그리고 rnum칼럼의 밑 칼럼(vOccup)은 rnum의 로직을 실행한 후 @vOccup변수에 a.Occupation(현재 읽힌 행의 Occupation)을 대입시켜 다음 행을 읽을 때 @vOccup이 바로 전 행의 a.Occupation정보를 담고 있도록 해주는 로직이다. </span></p>
<p><span>이런 로직이 성립되려면 반드시 ORDER BY를 통해 그룹화시키는 칼럼(OCCUPATION)으로 SORTING 해주어야 한다.</span></p>
<p><span>또한 반드시 (SELECT @vOccup:='', @rownum:=0 FROM DUAL)와 같이 우리가 쿼리 속에서 사용할 변수들을 초기화시켜 주어야 한다.</span></p>
<p><span>아래는 다음 쿼리의 결과이다.</span></p>
<pre class="language-sql"><code>Eve Actor 1 Actor 
Jennifer Actor 2 Actor 
Ketty Actor 3 Actor 
Samantha Actor 4 Actor 
Aamina Doctor 1 Doctor 
Julia Doctor 2 Doctor 
Priya Doctor 3 Doctor 
Ashley Professor 1 Professor 
Belvet Professor 2 Professor 
Britney Professor 3 Professor 
Maria Professor 4 Professor 
Meera Professor 5 Professor 
Naomi Professor 6 Professor 
Priyanka Professor 7 Professor 
Christeen Singer 1 Singer 
Jane Singer 2 Singer 
Jenny Singer 3 Singer 
Kristeen Singer 4 Singer 
</code></pre>
<p><span>의도한 대로 OCCUPATION 그룹마다 rownum이 생성되었다.</span></p>
<p>&nbsp;</p>
<blockquote><span>rnum을 그룹으로 묶어 직업 카테고리 별로 PIVOT 시키자.</span></blockquote>
<p>&nbsp;</p>
<p><span>위의 쿼리를 이해하려면 먼저 GROUP_CONCAT을 이해해야 한다. GROUP_CONCAT이란 같은 그룹에 속한 내용들 중 NULL값이 아닌 값들을 묶에 STRING으로 출력해주는 함수이다. </span></p>
<p><span>즉 다음과 같이 쿼리를 작성해보자.</span></p>
<pre class="language-sql"><code>SELECT
    GROUP_CONCAT(NAME),
    GROUP_CONCAT(OCCUPATION)
FROM
(
    SELECT a.*,
        (CASE @vOccup WHEN a.OCCUPATION THEN @rownum:=@rownum+1 ELSE @rownum:=1 END) rnum,
        (@vOccup:=a.OCCUPATION) vOccup
    FROM OCCUPATIONS a,(SELECT @vOccup:='', @rownum:=0 FROM DUAL) b
    ORDER BY OCCUPATION, NAME ) c
GROUP BY c.rnum

</code></pre>
<p><span>위의 쿼리를 rnum을 기준으로 그룹화시켜 GROUP_CONCAT을 NAME, OCCUPATION별로 뽑아 본 것이다.</span></p>
<pre class="language-sql"><code>Aamina,Christeen,Ashley,Eve Doctor,Singer,Professor,Actor 
Belvet,Jennifer,Julia,Jane Professor,Actor,Doctor,Singer 
Priya,Jenny,Britney,Ketty Doctor,Singer,Professor,Actor 
Samantha,Kristeen,Maria Actor,Singer,Professor 
Meera Professor 
Naomi Professor 
Priyanka Professor 
</code></pre>
<p><span>결과는 다음과 같다 rnum이 같은 것들끼리 묶인 이름과 직업들이 각각의 row 마다 출력된다.</span></p>
<p><span>이제 위의 쿼리에 조건문을 넣어 우리가 원하는 결과값을 출력해보자.</span></p>
<pre class="language-sql"><code>SELECT
    GROUP_CONCAT(if(Occupation = 'Doctor', Name, NULL)) AS 'Doctor', 
    GROUP_CONCAT(if(Occupation = 'Professor', Name, NULL)) AS 'Professor', 
    GROUP_CONCAT(if(Occupation = 'Singer', Name, NULL)) AS 'Singer', 
    GROUP_CONCAT(if(Occupation = 'Actor', Name, NULL)) AS 'Actor'
FROM
(
    SELECT a.*,
        (CASE @vOccup WHEN a.OCCUPATION THEN @rownum:=@rownum+1 ELSE @rownum:=1 END) rnum,
        (@vOccup:=a.OCCUPATION) vOccup
    FROM OCCUPATIONS a,(SELECT @vOccup:='', @rownum:=0 FROM DUAL) b
    ORDER BY OCCUPATION, NAME ) c
GROUP BY c.rnum
</code></pre>
<p><span>다음과 같이 각각의 직업별로 존재하면 이름을 출력하고 아니면 NULL을 출력하는 로직을 작성하여 출력하면 다음과 같이 우리가 원하는 결과물이 출력된다.🥳</span></p>
<pre class="language-sql"><code>Aamina Ashley Christeen Eve 
Julia Belvet Jane Jennifer 
Priya Britney Jenny Ketty 
NULL Maria Kristeen Samantha 
NULL Meera NULL NULL 
NULL Naomi NULL NULL 
NULL Priyanka NULL NULL 
</code></pre>
<p>&nbsp;</p>
<p><span>처음에는 PIVOT을 해보라길래 무슨 소리지? 의아했다. 사실 지금까지 업무를 하면서 PIVOT을 사용할 일이 없었기 때문이다. 이처럼 HackerRank를 사용하면 다양 한 부분을 연습해 볼 수 있어서 좋은 것 같다. 또 쿼리는 해보면 해볼 수록 더욱더 재미있는 것같다. 물론 나보다 더 좋은 해결 방법이 많이 있을 것이다 특히 HackerRank discussion 섹션에 가보면 다양한 해결책이 올라와 있으니 다들 심심하다면 HackerRank에서 문제를 풀어보는 것을 추천한다</span></p>
<p>&nbsp;</p>
<p><span>(참고로 Pivot 공부를 하면서 다음과 같은 웹사이트를 발견하였다. 다음 편에는 다음 웹사이트를 번역해보는 것으로 Pivot에 관하여 좀 더 공부를 해보아야겠다.)</span></p>
<p><a href="http://www.artfulsoftware.com/infotree/qrytip.php?id=78" target="_blank" rel="noopener"><span>Pivot에 대하여</span></a></p>
