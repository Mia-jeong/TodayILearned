# [MySQL] Projects

*다음은 hackerrank SQL section중 [Projects](https://www.hackerrank.com/challenges/projects/problem) 문제를 푸는 과정을 작성한 내용 입니다.*

Hackerrank에서 `medium` 레벨의 `Projects`  문제를 풀었다. 문제는 다음과 같았다.

> Projects 라는 테이블이 주어진다. 해당 테이블은 Task_ID, Start_Date, End_Date 컬럼을 포함하고 있다 하나의 row의 Start_Date와 End_Date는 각 각 1일씩 차이나는 것을 보장 한다. 즉 Start_Date가 `2015-10-01` 일 이면 End_Date 는 `2015-10-02` 일 이다. 만약 다른 데이터의 Start_Date가  현재 데이터의 End_Date 와 똑같다면 그건 똑같은 프로젝트이다. 즉,
>
> | Start_Date | End_Date   |
> | ---------- | ---------- |
> | 2015-10-01 | 2015-10-02 |
> | 2015-10-02 | 2015-10-03 |
>
> 위의 데이터는 같은 프로 젝트 이다.
>
> 공통 된 프로젝트의 시작과 종료일을 구하여라 (위의 데이터에서 시작일은 `2015-10-01` 종료일은 `2015-10-03` 이다.)
>
> 추출한 목록은 프로젝트 완료 기간을 기준으로 오름차순으로 정렬하여라. 만약 완료 기간이 같은 프로젝트가 있다면 시작일을 기준으로 오름차순으로 정렬 하여라.



#### ✍️ Solution

```mysql 
SET @end_date = '';
SET @group = 0;

SELECT MIN(START_DATE)
     , MAX(END_DATE)
  FROM (
        SELECT START_DATE
             , END_DATE
             , CASE @end_date 
               WHEN START_DATE 
               THEN @group:=@group 
               ELSE @group:=@group+1 
               END AS GROUP_NUM
             , @end_date:= END_DATE AS TEMP_END_NUM
          FROM Projects
```

나의 풀이법은 위와 같다. 사용자 정의 변수인 `@end_date` 와 `@group` 을 선언 해준 후, `END_DATE` 로 정렬된 쿼리에서 쿼리가 돌때마다 해당 데이터의 `END_DATE`를   `@end_date`  에 대입 시켜주고  `@end_date` 가 현재 데이터의  `START_DATE` 와 같으면   `@group`  숫자를 변경시키지 않고 다르다면  `@group` 을 1 증가시켰다.

이렇게 하여 동일 한 프로젝트 끼리 같은 `@group` 숫자를 부여하였다.

이후, `GROUP_NUM`  끼리 그룹지어 묶은 후, `MIN(START_DATE)` 와 `MAX(END_DATE)` 를 통해 정답을 구하였다. 



#### 🧐 후기

해당 문제는 `Advanced Join` 섹션에 있었는데 나의 Solution은 Join을 전혀 사용하지 않았다. 그래서 `Discussion` 을 살펴보기로 하였다.

```mysql 
SELECT Start_Date, MIN(End_Date)
FROM 
    (SELECT Start_Date FROM Projects WHERE Start_Date NOT IN (SELECT End_Date FROM Projects)) a,
    (SELECT End_Date FROM Projects WHERE End_Date NOT IN (SELECT Start_Date FROM Projects)) b 
WHERE Start_Date < End_Date
GROUP BY Start_Date
ORDER BY DATEDIFF(MIN(End_Date), Start_Date) ASC, Start_Date ASC;
```

해당 Soultion은 `UNION ALL` 을 통해 JOIN한 후 데이터를 뽑는 형식이었다. `a` 와 `b` 쿼리를 각각 살펴보면 `a` 는 End_Date와 일치하지 않는 Start_Date 들을 구하는 쿼리이며,  `b` 는 Start_Date와 일치하지 않는 End_Date들을 구하는 쿼리이다.

Union All은 기준이 되는 데이터 하 나 당 전체 데이터를 각각 조인 하기 때문에 다음과 같이

`WHERE Start_Date < End_Date ` 조건을 걸어 주었다. 왜냐하면 모든 Start_Date는 End_Date 이전 일이기 때문이다. 

하지만 해당 쿼리는 Start_Date가 End_Date보다 작은 모든 데이터를 추출 할 것이므로 그중에서 서로 동일한 프로젝트의 시작일과 종료일을 매칭 시켜주어야 한다. 

그렇기 때문에 Start_Date로 그룹을 묶어 준 후 해당 그룹에서 최소 값  `MIN(End_Date)`  을 구하는 로직을 추가 한 것이다. 해당 쿼리 대로 작성하니 사용자정의 변수를 사용하지 않아도 되어서 좀더 깔끔한 것 같았다.

