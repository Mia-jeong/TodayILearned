<h1><a name="header-n70" class="md-header-anchor md-print-anchor" href="af://n70"> </a><span>Mysql group by, order by 숫자로 사용하는 방법</span></h1>
<p><span>Hackker rank 에서 문제를 풀다가 group by 와 order by를 숫자로 사용하는 방법을 알게 되었다.</span></p>
<p><span>문제는 다음과 같이 각각의 직원에 대해서 일한 달(months)과 월급(salary)을 곱한 총 급여금액중 최대값을 구하는 간단한 문제였다.</span></p>
<figure><table>
<thead>
<tr><th><span>employee_id</span></th><th><span>name</span></th><th><span>months</span></th><th><span>salary</span></th></tr></thead>
<tbody><tr><td><span>12228</span></td><td><span>Rose</span></td><td><span>15</span></td><td><span>1968</span></td></tr><tr><td><span>33645</span></td><td><span>Angela</span></td><td><span>1</span></td><td><span>3443</span></td></tr><tr><td><span>45692</span></td><td><span>Frank</span></td><td><span>17</span></td><td><span>1608</span></td></tr></tbody>
</table></figure>
<p><span>( 데이터 이하 생략 )</span></p>
<p>&nbsp;</p>
<h3><a name="header-n96" class="md-header-anchor md-print-anchor" href="af://n96"> </a><span>1. 나의 Solution</span></h3>
<pre><code class='language-sql' lang='sql'>SELECT Max(salary*months), count(*)
  FROM Employee
 WHERE salary*months in (SELECT MAX(salary*months)
                           FROM Employee)
</code></pre>
<p><span> 처음에 나는 다음과 같이 subquery를 사용하여 문제를 해결 하려고 하였다. </span></p>
<p><span>이후, Discussion 패널에 들어가보니 사람들이 다양한 방식으로 문제를 해결 한 것을 볼 수 있었다.</span></p>
<p>&nbsp;</p>
<h3><a name="header-n101" class="md-header-anchor md-print-anchor" href="af://n101"> </a><span>2. Group by, Order by 를 숫자로 지정</span></h3>
<pre><code class='language-sql' lang='sql'>SELECT (salary * months)as earnings ,count(*)
  FROM employee
 GROUP BY 1
 ORDER BY 1 DESC LIMIT 1
</code></pre>
<p><span>위의 쿼리를 보면 GROUP BY 와 ORDER BY 에 숫자 1을 사용하였다. 여기서 1이란 salary*months 를 한 후 해당 데이터를 Alias를 통해 earnings 으로 지정해준 컬럼을 의미한다. </span></p>
<p><span>즉, 쿼리를 작성할때 뽑고 싶은 컬럼의 인덱스를 (1~ ) 를 GROUP BY 와 ORDER BY에 사용 할 수 있다.</span></p>
<h3><a name="header-n105" class="md-header-anchor md-print-anchor" href="af://n105"> </a><span>3. Group by, Order by 에 Alias지정 </span></h3>
<p><span>또한, 다음과 같이 Group by 와 Order by 에 Alias 를 지정 할 수 있다.</span></p>
<pre><code class='language-sql' lang='sql'>SELECT (salary * months)as earnings ,count(*)
  FROM employee
 GROUP BY earnings
 ORDER BY earnings DESC LIMIT 1
</code></pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
