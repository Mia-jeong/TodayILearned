<h1><a name="header-n262" class="md-header-anchor md-print-anchor" href="af://n262"> </a><span>MySql 로 Median 값 구하기</span></h1>
<p><span> *Median : 중간 값.</span></p>
<p><span>Hackerrank 의 Aggregation 문제를 풀던 중 중간 값을 구하는 문제를 접하게 되었다.</span></p>
<p>&nbsp;</p>
<h3><a name="header-n266" class="md-header-anchor md-print-anchor" href="af://n266"> </a><span>1. 문제 </span></h3>
<p><span>(문제) 다음 STATION테이블에서 LAT_N 컬럼 값의 중간 값을 구하시오.</span></p>
<figure><table>
<thead>
<tr><th><span>Field</span></th><th><span>Type</span></th></tr></thead>
<tbody><tr><td><span>ID</span></td><td><span>NUMBER</span></td></tr><tr><td><span>CITY</span></td><td><span>VARCHAR2(21)</span></td></tr><tr><td><span>STATE</span></td><td><span>VARCHAR2(2)</span></td></tr><tr><td><span>LAT_N</span></td><td><span>NUMBER</span></td></tr><tr><td><span>LONG_W</span></td><td><span>NUMBER</span></td></tr></tbody>
</table></figure>
<p>&nbsp;</p>
<h3><a name="header-n288" class="md-header-anchor md-print-anchor" href="af://n288"> </a><span>2. 나의 Solution</span></h3>
<p><span>처음 내가 사용한 솔루션은 다음과 같았다.</span></p>
<pre><code class='language-sql' lang='sql'>SET @row:= 0;

SELECT ROUND(LAT, 4)
  FROM (
SELECT LAT_N AS LAT,
       @row:=@row+1 AS R_NUM
  FROM STATION
 ORDER BY 1 DESC
) A
WHERE R_NUM = (SELECT ROUND(COUNT(*)/2) FROM STATION)
</code></pre>
<p><span>우선, row 라는 사용자정의 변수를 선언해 준 후 WHERE 절에서 전체 데이터 갯수의 나누기 2한 값으로 row를 비교해준 후 일치하는 값의 LAT를 뽑아 주는 것이다.</span></p>
<p><span>이렇게 제출 한 결과 검사에는 무난히 통과 할 수 있었다. </span>
<span>❗️ 그.러.나 이게 통과한 이유는 해당 데이터의 갯수가 499개 즉 &quot;홀수&quot; 였기 때문이다.</span></p>
<p><span>즉 499 / 2 를 하면 249.5가 나오고 ROUND를 시켰기 때문에 250번째 row 의 값을 출력하여 알맞은 값을 출력 할 것이다. 그렇다면 500개의 즉, 짝수개의 데이터가 나오면 어떻게 할까? 중간 값은 250번째 데이터와 251번째 데이터를 더한 값의 평균값이 바로 Median (중간 값) 이 될 것이다.</span></p>
<p><span>⭕️ 그래서 다음과 같은 로직을 추가 하였다.</span></p>
<pre><code class='language-mysql' lang='mysql'>SET @row:= 0;

SELECT ROUND(AVG(LAT), 4)
  FROM (
SELECT LAT_N AS LAT,
       @row:=@row+1 AS R_NUM
  FROM STATION
 ORDER BY 1 DESC
) Z
WHERE R_NUM = (SELECT CEIL(COUNT(*)/2) FROM STATION)
  OR  R_NUM = (SELECT FLOOR(COUNT(*)/2+1) FROM STATION)

</code></pre>
<p><span>위의 쿼리가 첫 번째 쿼리와 달라진 점은 다음과 같이 두가지다</span></p>
<ol>
<li><span>LAT를 뽑을때 앞에 AVG (평균 구하는 함수)를 추가</span></li>
<li><span>WHERE 절에서 R_NUM을 비교하는 값에 OR조건을 추가하여 두가지 조건을 비교해줌</span></li>

</ol>
<p><span>우선 2 번 부터 확인해보자. 왜 R_NUM을 비교할 시에 두가지 조건으로 조건을 추가 해 줬을까? </span></p>
<blockquote><p><span>홀수</span></p>
</blockquote>
<p><span>데이터가 499개 있다고 생각해보자. 499/2 즉, 249.5 를 올림 한 값은 250 이다. 또한 499/2+1 즉, 250.5 를 내림한 값 역시 250이다. 따라서 홀수 일 경우 뽑히는 값은 250인덱스 하나 일것이다. 이후 해당 값을 AVG한 값을 구하면 250번째 인덱스 값이 그대로. 출력 될것 이다.</span></p>
<blockquote><p><span>짝수</span></p>
</blockquote>
<p><span>그렇다면 짝수 일때는 어떠할까? 데이터가 500개가 존재한다고 생각해보자. 500/2 =250의 올림 값은 250, 500/2+1 = 251 값의 내림값은 251이다. 따라서 250 인덱스 값과 251의 인덱스 값의 LAT 값의 평균(AVG)를 구하면 중간 값이 나온다.</span></p>
<p>&nbsp;</p>
<h3><a name="header-n310" class="md-header-anchor md-print-anchor" href="af://n310"> </a><span>3. Disccusion 에서 본 쿼리</span></h3>
<p><span>다른 해결책이 없을까 궁금해서 Disccustion을 둘러보다 다음과 같은 쿼리를 발견 하였다.</span></p>
<pre><code class='language-mysql' lang='mysql'>SELECT ROUND(S.LAT_N,4) MEDIAN 
  FROM STATION S
 WHERE (SELECT COUNT(LAT_N) FROM STATION WHERE LAT_N &lt; S.LAT_N ) = 
       (SELECT COUNT(LAT_N) FROM STATION WHERE LAT_N &gt; S.LAT_N)
</code></pre>
<p><span>위의 쿼리의 WHERE절을 자세히 봐보자. 즉. 데이터 갯수가 총 5개가 있고 LAT_N값은 각각 [1, 2, 3, 4, 5] 라고 생각해 보자. 쿼리가 동작 할때 WHERE절은 데이터 한줄 한줄 비교하게 되는데  전체 데이터 LAT_N의 값들 중에 현재 S.LAT_N 값인 1 보다 작은 값은 0개 이며 S.LAT_N보다 큰 값은 4개이다.</span></p>
<p><span>S.LAT_N이 2인 경우 작은 값은 1개 큰 값들은 3개이다. 그 다음 S.LAT_N이 3인 경우를 생각해보자. S.LAT_N보다 작은 값들은 2개, 큰값들 역시 2개이다 이때 작은 값들의 갯 수와 큰 값들의 갯수 역시 2개이므로 해당값이 전체 데이터 값은 중간 값이 된다.</span></p>
<p><span>❗️하지만 해당 쿼리 역시 홀수에서만 작동 되고 짝수 갯수에는 올바르게 작동 되지 않을 것이다.</span></p>
<p>&nbsp;</p>
