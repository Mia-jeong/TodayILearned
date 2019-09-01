# [MYSQL] 15 Days of Learning SQL

*다음은 [hackerrank SQL section중 15 Days of Learning SQL](https://www.hackerrank.com/challenges/15-days-of-learning-sql/problem) 문제를 푸는 과정을 작성한 내용 입니다.*

hackerrank에서 SQL문제를 풀다 드디어 난이도가 `hard` 인 문제를 마주하게 되었다. 난이도가 높은 만큼 생각보다 만만 치 않은 문제였다.

문제 내용은 다음과 같았다.

>  Julia는 15일동안 배우는 SQL 컨테스트를 개최하였다. 해당 컨테스트는 2016년 3월 1일 부터 2016년 3월 15일 까지 진행 된다.
>
> 컨테스트가 진행되는 동안 각각의 날짜를 기준으로 시작일 부터 적어도 1문제 이상을 제출 한 총 유저들의 수를 구하여라. 그리고 그날 가장 문제를 가장 적게 제출 한 유저의 아이디와 이름을 구하여라. 만약 가장 적게 문제를 제출한 유저가 2명이상일 경우 해당 유저의 아이디(hacker_id)를 내림차순으로 가장 첫번째 유저의 정보를 구하여라. 해당 쿼리의 결과는 날짜, 유저의 수, 유저아이디, 이름 으로 컬럼이 구성되어 있어야 하며 date 순서대로 정렬 되어 있어야 한다.



각각의 날짜와 그날 마다 제출한 문제수가 가장 적은 유저와 이름을 구하는건 어렵지 않았다. 하지만 문제는 각각의 날짜를 기준으로 시작일 부터 적어도 한 문제 이상을 제출한 유저를 구하는 것이었다.

##### 📌시작일 부터 기준이 되는 날짜 까지 매일 문제를 제출한 유저의 수를 구해보자.

그래서 먼저 다른 조건은 생각하지 않고 해당 정보만 추출해 보고자 하였다.

```mysql
 SELECT COUNT(distinct hacker_id)  
         FROM Submissions X 
         WHERE X.submission_date = '2016-03-02'
           AND (SELECT COUNT(distinct Y.submission_date)                                                            									FROM Submissions Y
                 WHERE X.hacker_id = Y.hacker_id                                                               										AND Y.submission_date < X.submission_date)                                                            												= DATEDIFF(X.submission_date , '2016-03-01')
```

먼저 메인 쿼리 `X`를 작성한다. 이후 WHERE조건을 작성하는데

첫번째로,  기준이 되는 날짜와 `2016-03-02`  일치하는 날짜를 가진 아이디를 구한다`X.submission_date = '2016-03-02'`. 

하지만 여기서 마무리 하면 `2016-03-02` 에 문제를 제출한 유저만 뽑힐 것이다. 그렇기 때문에 시작일`2016-03-01`부터 매일  적어도 하나 이상의 문제를 제출한 유저를 뽑아야 한다.

두번째로,  서브 쿼리`Y`를 작성 하자. 우선 서브쿼리 `Y` 에서 기준이 되는 날짜에 제출한 이력이 있는 hacker_id를 가져오기 위해 다음과 같은 조건을 추가하자.`X.hacker_id = Y.hacker_id   `. 

그 이후 해당 유저가  `X` 의 submission_date보다 이 전의 날짜에 제출한 이력이 있는 데이터를 뽑아내기 위하여 다음과 같이 `Y.submission_date < X.submission_date` 조건문을 제시하고 

그 유저가 문제를 제출한 날짜(중복X) 의 총 수를 `DATEDIFF(X.submission_date , '2016-03-01')` 다음과 같이 `DATEDIFF` 함수를 통해 일치시키는 조건을 추가하자. 

즉, 3월1일, 3월 2일 두 날짜 모두 문제를 제출했다면 `COUNT(distinct Y.submission_date)` 은 1일 나올 것이고 `DATEDIFF(X.submission_date , '2016-03-01’)` 여기에서 `X.submission_date` 는 `2016-03-02` 가 되므로 역시 1이 나와 조건을  `=` 만족 시킬 것이다.

##### 📌 각각의 날짜 와 함께 위에서 가져온 유저의 총 수를 가져오는 쿼리를 작성해보자.

```mysql
SELECT A.submission_date,
       (SELECT COUNT(distinct hacker_id)  
               FROM Submissions X 
               WHERE X.submission_date = A.submission_date
                 AND (SELECT COUNT(distinct Y.submission_date)                                                            											  FROM Submissions Y
                  		 WHERE X.hacker_id = Y.hacker_id                                                               												  AND Y.submission_date < X.submission_date)                                                            												= DATEDIFF(X.submission_date , '2016-03-01'))
 FROM (SELECT distinct submission_date
         FROM Submissions ) A
```

각각의 날짜를 중복없이 뽑아야 하기 때문에 다음과 같이 `(SELECT distinct submission_date
         FROM submissions ) A` 를 통해 date를 가져오는 메인 쿼리를 작성한 후, 하드코딩으로 submission_date 부분을 일치시켜줬던 부분에 다음과 같이 `X.submission_date = A.submission_date` 를 넣어주자.



##### 📌각각의 날짜마자 제일 적은 수의 문제를 제출한 유저의 아이디와 이름을 가져오는 쿼리를 작성해보자.

```mysql
SELECT A.submission_date,
       (SELECT COUNT(distinct hacker_id)  
               FROM Submissions X 
               WHERE X.submission_date = A.submission_date
                 AND (SELECT COUNT(distinct Y.submission_date)                                                            											  FROM Submissions Y
                  		 WHERE X.hacker_id = Y.hacker_id                                                               												  AND Y.submission_date < X.submission_date)                                                            												= DATEDIFF(X.submission_date , '2016-03-01')),
      (SELECT hacker_id
         FROM Submissions Z
        WHERE Z.submission_date = A.submission_date
       GROUP BY hacker_id
       ORDER BY count(hacker_id) DESC, hacker_id ASC 
       LIMIT 1) AS min_hacker_id,
      (SELECT name
         FROM Hackers
        WHERE hacker_id = min_hacker_id)
 FROM (SELECT distinct submission_date
         FROM Submissions ) A
```

10번째 줄부터가 해당 조건을 만족 시키는 쿼리의 내용이다. 우선 `Z.submission_date = A.submission_date` 해당 날짜에 문제를 제출한 유저의 정보를 구한 후 해당유저들을 그룹으로 묶는다. `GROUP BY hacker_id` 그 이후, `count(hacker_id)` 그룹으로 묶인 유저들이 그날 총 몇개의 문제를 제출했는지 갯수를 토대로 내림차순으로 먼저 정렬을 한 후 겹치는 갯수가 발생할 경우를 대비하여 `hacker_id ASC ` hacker_id를 오름차순으로 정렬해 준다. 그 이후 `LIMIT 1` 을 통해 제일 첫번째 데이터를 가져온다. 

이 후, 해당 유저의 이름을 가져오기 위해 다음 `Hackers` 테이블에서 위에서 가져온 hacker_id와 일치하는 유저의 이름 정보를 가져온다 .`SELECT name FROM Hackers WHERE hacker_id = min_hacker_id)`



##### 🧐 후기

사실 처음 문제를 접했을때는 금방 풀 수 있을 줄 알았는데 앞서 말했듯이 시작일부터 기준일까지 매일 문제를 작성한 유저의 수를 구하는데 좀 애를 먹었다. 특히 메인쿼리의 컬럼이 서브쿼리의 어디까지 영향을 끼칠 수 있는지 좀 더 공부를 해봐야겠다고 느끼게 해준 문제이다. 시간이 나면 다른 사람은 어떻게 풀었는지 분석해보는 포스트를 작성해보아야겠다. 사실 나의 쿼리가 속도면에서 좋아보이지 않기 때문이다. SQL 튜닝 부분에 대해서도 어느정도 SQL에 대해 좀더 자신감이 붙으면 같이 공부해 보아야 겠다.
