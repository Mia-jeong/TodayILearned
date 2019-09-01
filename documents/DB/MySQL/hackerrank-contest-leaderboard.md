# Contest Leaderboard

*다음은 hackerrank SQL section중 [Contest Leaderboard](https://www.hackerrank.com/challenges/contest-leaderboard/problem) 문제를 푸는 과정을 작성한 내용 입니다.*



Hackerrank 에서 `medium` 레벨인 `Contest Leaderboard` 문제를 풀어 보았다. 해당 문제는 medium 보다는 easy에 속하는 문제 같았다. 간단한` Join` 과` Group by` 를 통해 손 쉽게 결과를 도출 할 수 있었다.

문제는 다음과 같았다.

> 각각의 유저가 제출한 모든 문제들 에 대한 점수중 최고 점수만을 구해 합계를 구하라. 점수의 총합은 내림차순으로 정렬 되어야 하며 만약 똑같은 합계점수를 가진 유저가 한 명 이상 존재하는 경우 hacker_id의 오름차순으로 정렬하여라.  총 합계 점수가 0인 유저는 목록에서 제외 시켜라.
>
> (테이블에 관한 정보는 위의 실제 문제 링크에서 확인하는 것을 추천 드립니다.)



#### ✍️ Solutions

```mysql 
SELECT A.hacker_id, MAX(B.name), SUM(A.score) 
  FROM (SELECT hacker_id, challenge_id, MAX(score) AS score
          FROM submissions
         GROUP BY hacker_id, challenge_id) A
 INNER JOIN Hackers B
          ON A.hacker_id = B.hacker_id
 GROUP BY A.hacker_id
 HAVING sum(A.score) > 0
 ORDER BY SUM(A.score) DESC, A.hacker_id ASC
```



먼저, `submissions `테이블에서  hacker_id와 challenge_id로 그룹을 지어준 후 각각의 유저가 제출한 각각의 문제에 대하여 최고 점수만을 가져오는 메인 쿼리  `A` 를 작성 하였다.

그 이후, 해당 유저의 이름을 구하기 위해 `Hackers` 테이블과 `INNER JOIN` 을 시켜 유저에 대한 이름을 가져 오도록 하였다.

마지막으로 `A` 쿼리로 작성된 데이터를 `GROUP BY`를 통해 다시 `hacker_id` 를 통해 그룹으로 묶은 이후 총 합계가 0인 유저를 제외시키기 위해 `HAVING sum(A.score) > 0` 다음과 같은 조건을 추가 해 주었다. 이 후, 먼저 총 합계 점수에 대해서 내림차순 , 그 이후 hacker_id 에 대하여 오름차순으로 데이터를 정렬 하였다.



#### 🧐 후기

`Discussion ` 을 들어가보니 대부분 나와 같은 방식으로 푼 것 같았다. 만약 똑같은 점수를 가진 유저가 있다면 그 중 hacker_id가 더 낮은 유저를 구하라 라는 조건 이 붙었다면 쿼리가 좀더 복잡해지지 않았을까 싶었고 실제로 한 번 쿼리를 작성 해 보았다

```mysql 
SET @rank=0;
SET @max_sum=0;

SELECT hacker_id
     , name
     , tsum
  FROM (
        SELECT hacker_id
             , name
             , tsum
             , (CASE @max_sum WHEN tsum THEN @rank:=@rank+1 ELSE @rank:=1 END) rnum
             , (@max_sum:=tsum) m_sum
         FROM
            (SELECT A.hacker_id
                  , MAX(B.name) as name
                  , SUM(A.score) as tsum
              FROM (SELECT hacker_id, challenge_id, MAX(score) AS score
                      FROM submissions
                     GROUP BY hacker_id, challenge_id) A
             INNER JOIN Hackers B
                      ON A.hacker_id = B.hacker_id
             GROUP BY A.hacker_id
             HAVING sum(A.score) > 0) X
         ORDER BY tsum DESC, hacker_id ASC ) Y
 WHERE rnum = 1
 ORDER BY tsum DESC
```

쿼리가 좀 지저분 해졌는데 일단 나의 솔루션은 총 합계 점수와 hacker_id로 정렬한 후, `@rank` 와 `@max_num` 이라는 변수를 생성 하여 다음과 같이 조건

`(CASE @max_sum WHEN tsum THEN @rank:=@rank+1 ELSE @rank:=1 END) rnum
, (@max_sum:=tsum) m_sum`

을 달아서 총 합계 점수가 같은 유저들 끼리 rank 를 구하였다.

이 후 `rank = 1` 인 유저만을 선택하여 최종 목록을 추출 하였다. 해당 쿼리는 원래 문제의 정답이 아니기 때문에 더 좋은 솔루션을 찾아보고 싶었지만 Discussion  에서는 원래 문제에 대한 정답만을 토론하는 곳이기에 답을 구할수 없었다. 


