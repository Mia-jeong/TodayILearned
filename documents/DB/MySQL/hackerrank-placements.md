# Placements

*다음은 hackerrank SQL section중 [Placements](https://www.hackerrank.com/challenges/placements/problem) 문제를 푸는 과정을 작성한 내용 입니다.*



Hackerrank 에서 `medium` 레벨인 `Placements` 문제를 해결 하였다. 해당 문제는 `JOIN` 을 사용하여 데이터를 잘 추출할 수 있는지 확인하는 문제 였다.

문제는 다음과 같았다.

> 다음과 같이 Student, Friends, Packages 3가지 테이블이 주어진다. Students 테이블은 ID와 NAME 두 가지의 컬럼을 가지고 있으며 Friends는 ID와 Friend_ID 두 가지 컬럼을 가지고 있다. Packages 테이블은 ID와 Salary 테이블을 가지고 있다.
>
> 친구의 Salary 보다 적은 Salary를 받는 학생의 이름을 구하시오. 단 친구의 Salary 의 오름차순으로 정렬을 해야 한다.



#### ✍️Solution

```mysql 
SELECT A.NAME
  FROM Students A
 INNER JOIN Friends B
    ON A.ID = B.ID
 INNER JOIN Packages C
    ON A.ID = C.ID
 INNER JOIN Packages D
    ON B.Friend_ID = D.ID
 WHERE C.Salary < D.Salary
 ORDER BY D.Salary
```

나는 다음과 같이 여러번의 조인을 통해 학생의 `C.Salary` 와 해당 학생의 친구의 `D.Salary` 를 구하여 비교하는 방식으로 데이터를 추추 하였다.



#### 🤔 후기

사실 단순 JOIN을 요구하는 문제라 딱히 어려움은 없었다. 하지만 `Discussion` 에서 다음과 같은 쿼리를 발견 하였다.

```mysql 
Select S.Name
From ( Students S join Friends F Using(ID)
       join Packages P1 on S.ID=P1.ID
       join Packages P2 on F.Friend_ID=P2.ID)
Where P2.Salary > P1.Salary
Order By P2.Salary;
```

나와 같이 JOIN을 사용하였지만 문법이 조금 달랐다. 사실 Join 할때 `USING`이라는 명령어를 사용하여 데이터 값을 일치시키는건 해당 쿼리를 보고 처음 알게 되었다.😅 나는 항상 `ON` 을 써서 데이터가 일치하는 JOIN문을 작성했는데 저렇게 하니 쿼리가 좀더 간결해 지는 거 같았다. 

