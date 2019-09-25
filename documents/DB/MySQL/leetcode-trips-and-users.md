# [JOIN, COUNT] Leetcode - Trips and Users

*다음은 leetcode Database section중 Trips and Users문제를 푸는 과정을 작성한 내용 입니다.*

Leetcode에서 **hard** 레벨인 **[Trips and Users](https://leetcode.com/problems/trips-and-users/)** 문제를 풀어보았다. **JOIN** 과 **COUNT, IF** 를 통해 결과를 도출해 내었다.

문제는 다음과 같다.

> Trips 테이블은 택시 여행에 관련한 정보들을 담고 있는 테이블이다. 각각의 여행에 대하여 고유ID, Client_Id, Driver_Id, City_Id, Status, Request_at의 정보를 가지고 있으며 Client_Id, Driver_Id 는 Users테이블의 외래키이다.
>
> Users테이블은 각각의 사용자에 대한 정보를 담고 있으며 Users_Id, Banned, Role의 정보를 담고있다.
> 참고로 Trips테이블의 Status와 Users테이블의 Role은 ENUM형식이며 각각
> Status : ‘completed’, ‘cancelled_by_driver’, ‘cancelled_by_client’
>
> Role: ‘client’, ‘driver’, ‘partner’
>
> 정보를 가지고 있다.
>
> 2013-10-01 일 부터 2013-10-03일 까지 Banned되지 않은 유저(해당 컬럼의 정보가 'No')들의 각각 날짜의 취소율을 구하여라.

### ✍️ Solution

```mysql
Select A.Request_at as Day, 
       ROUND(count(if(Status != 'completed', Status, null))/count(Status), 2) as 'Cancellation Rate'
  from Trips A
 inner join Users B
    on A.Client_Id = B.Users_Id and B.Banned = 'No'
 inner join Users C
    on A.Client_Id = C.Users_Id and C.Banned = 'No'
  where Request_at between '2013-10-01' and '2013-10-03'
  group by Request_at
  order by Request_at
```

내가 작성한 쿼리는 다음과 같다.

우선 Trips테이블을 메인쿼리로 정한 후 Users 테이블을 Join시켜 Banned되지 않은 유저들의 정보들을 출력하였다. 이후 between을 통해 Request_at 를 2013-10-01~2013-10-03으로 한정 짓고 Group by를 통해 날짜 별로 그룹지어 줬다.

이후 COUNT 와 IF 함수를 통해 취소(Status != 'completed ' /전체 ) 율을 계산 후 Round 함수를 통해 소수점 2자리까지 반올림 해주었다.

### 🧐후기

이번 쿼리를 작성하면서 COUNT 안에 IF 함수를 작성할 수 있다는 걸 새롭게 알게 되었다. 사실 그 전에 쿼리를 공부하다가 본적이 있는데 직접 사용해본적은 이번이 처음이다. 😎