# JOIN - Human Traffic of Stadium

*다음은 leetcode Database section중 Human Traffic of Stadium 문제를 푸는 과정을 작성한 내용 입니다.*

Leetcode에서 **hard** 레벨인 **Human Traffic of Stadium** 문제를 풀어보았다. **JOIN** 과 **WHERE** 을 통해 결과를 도출해 내었다.

문제는 다음과 같았다.

> X 시는 새로운 스타디움을 건설하였다. 해당 스타디움에는 매일매일 방문 하는 사람들과 그 날짜를 기록해 놓으며 id, visit_date, people로 데이터를 분류하여 저장한다. 
>
> 3일 이상 연속적인 날짜에 사람들이 매일 100명이상 방문한 데이터들을 출력하여라.
>
> 참고로 매일 매일은 무조건 row가 한개밖에 없으며 id와 같이 증가한다.

### ✍️ Solution

```mysql
select distinct a.id,  a.visit_date, a.people
  from stadium a, stadium b, stadium c
 where a.people >= 100 and b.people >= 100 and c.people >= 100
   and ((a.id = b.id -1 and b.id = c.id -1) 
       or (a.id = b.id + 1 and a.id = c.id -1)  
       or (a.id = b.id + 1 and b.id = c.id + 1) ) 
  order by a.id
```

우선 해당 데이터를 뽑기위해 stadium은 a, b, c로 join 시켜주었다. 3개를 join시킨 이유는 조건에 3일이상 연속적인 날짜들을 출력하라고 되어있기 때문이다.

그 이후 다음과 같은 조건을 걸어 주었다.

1. a.people >= 100 and b.people >= 100 and c.people >= 100 : 사람들이 100명 이상인 데이터들을 각각의 테이블에서 뽑아준다.
2. 경우의 수를 계산하여 조건문을 걸어준다.
   - (a.id = b.id -1 and b.id = c.id -1) : a = 1, b = 2, c = 3 인 경우
   - (a.id = b.id + 1 and a.id = c.id -1)  : a = 2, b = 1, c = 3 인 경우
   - (a.id = b.id + 1 and b.id = c.id + 1) : a = 3, b = 2, c = 1 인 경우
3. Order by 를 통해 a.id 를 오름차순으로 정렬 
4. 겹치는 데이터가 없게 distinct 를 통해 데이터를 출력한다.

### 🧐 후기

약간의 하드코딩 느낌이 나지만 더 좋은 방법이 일단은 생각나지 않기에 저렇게 작성하였다. 이후, 좀더 좋은 solution이 생각나면 좀더 적어보아야겠다.