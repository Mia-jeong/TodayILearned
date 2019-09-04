# Symmetric Pairs

*다음은 hackerrank SQL section중  [Symmetric Pairs](https://www.hackerrank.com/challenges/symmetric-pairs/problem) 문제를 푸는 과정을 작성한 내용 입니다.*

Hackerrank 에서 `medium` 레벨의 Symmetric Pairs 문제를 풀어보았다 해당 문제는 `JOIN` 을 사용하여 원하는 데이터를 뽑을 수 있는지 확인 하는 문제였다. 문제는 다음과 같았다.



> 다음과 같이 X, Y 컬럼을 가지고 있는 Functions 테이블이 있다.
>
> 해당 데이터 중에 Symmetric pairs 즉 (X1, Y1), (X2, Y2) 를 구하여라. Symmetric pairs란 X1 = Y2, Y1 = X2 를 의미 한다. 
>
> 추출 한 데이터를 X를 기준으로 오름차순으로 정렬 하라.



#### ✍️Solution

```mysql 
SELECT A.X, A.Y 
  FROM Functions A
 INNER JOIN Functions B
    ON A.X = B.Y AND A.Y = B.X
 GROUP BY A.X, A.Y
HAVING A.X < A.Y OR COUNT(A.X) > 1
 ORDER BY A.X ASC
```

쿼리를 설명하면 다음과 같다.

1. 먼저 Functions `A` 테이블과 Function `B` 테이블을 `INNER JOIN` 을 통해 `A.X = B.Y AND A.Y = B.X` 다음과 같은 조건을 달아주어  Symmetric Pair의 가능성이 있는 데이터들을 뽑아온다 하지만 해당 데이터들은 즉 (20, 21), (21, 20) 중복되는 데이터 혹은 (10, 10) 과 같이 Symemtric Pair는 아니지만 X 와 Y가 같아서 뽑아오는 데이터들  포함하고 있을 것이다. 
2. 중복되는 데이터를 없애주기 위해 `GROUP BY A.X, A.Y` 다음과 같이 그룹으로 묶어주다. 해당 문장을 통해 (30, 30), (30, 30) 이런식으로 X와 Y가 서로 같은 Symmetric Pair들은 하나씩 만 나오게 될것이다.
3. 그 이후 그룹으로 묶어준 데이터에 `HAVING COUNT(A.X) > 1 or A.X < A.Y`  다음과 같은 조건을 걸어 준다.
   - `A.X < A.Y` 란 예를 들어 `(20, 21), (21, 20)` 이런식으로 X, Y가 서로 다를 경우 X를 순서대로 오름 차순하므로 `(20, 21)` 데이터만 추출해야 한다. 그렇기 때문에 다음과 같은 조건을 넣어 주는 것이다.
   - `COUNT(A.X) > 1` 이란 위의 조건만 달 았을 경우 `(30, 30), (30, 30)` 과 같이 X와 Y가 같은 Symmetric Pair는 뽑히지 않는 경우를 예방하기 위해 넣어 준 조건이다. 또한 Symmetric Pair는 아니지만 `(10, 10)` 이런 식으로 X와 Y가 같아서 뽑혀진 데이터 들 역시 걸러 줄수 있다.
4. 마지막으로 X를 기준으로 오름차순 정렬을 해주자.



#### 🧐 후기

생각 보다 간단할 줄 알았는데 오래 걸린 문제이다.  중복되는 데이터 포함 Symmetric Pair 전체 리스트를 뽑아오는건 INNER JOIN으로 쉽게 해결을 했으나 문제는 그 다음 부터 였다. 가져온 리스트중  Pair에 속하는 데이터일 경우 중복을 제거 하고 둘중 하나의 데이터만 추출하여야 했는데 이 부분 때문에 조금 애를 먹었다. 그래도 재미있는 문제 였다.
