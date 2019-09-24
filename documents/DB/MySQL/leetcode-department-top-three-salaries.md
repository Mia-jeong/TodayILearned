# JOIN - Department Top Three Salaries

*다음은 leetcode Database section중 Human Traffic of Stadium 문제를 푸는 과정을 작성한 내용 입니다.*

Leetcode에서 **hard** 레벨인 **[Department Top Three Salaries](https://leetcode.com/problems/department-top-three-salaries/)** 문제를 풀어보았다. **JOIN** 과 **사용자 정의 변수** 를 통해 결과를 도출해 내었다.

문제는 다음과 같았다.

> Employee 테이블은 모든 Employee 의 Id, Name, Salary, DepartmentId의 정보를 저장한다. Department테이블은 회사의 모든 부서의 Id와 Name을 저장한다 Department 테이블의 Id와 Employee 테이블의 DepartmentId은 서로 연결되어 있다.
>
> 각각의 부서의 상위 3위 내의 Salary를 받고 있는 직원들의 데이터를 출력하시오. 출력데이터는 Departmen(부서 이름), Employee(직원 이름), Salary(월급) 으로 출력하시오.

### ✍️ Solution

```mysql
select b.Name as Department,
       a.Name as Employee,
       a.Salary
  from (
            select DepartmentId, 
                   Name, 
                   Salary,
                   case 
                   when DepartmentId = @temp_dept
                   then 
                        case 
                        when @temp_sal > Salary
                        then @curRank:= @curRank +1
                        else @curRank:= @curRank
                        end
                   else @curRank:=1
                   end as rank,
                   (@temp_dept :=DepartmentId) as temp_dept,
                   (@temp_sal := Salary) as temp_sal
              from Employee , (SELECT @curRank := 0, @temp_dept := -1, @temp_sal:= -1) r
             order by DepartmentId ASC, Salary DESC ) a
  inner join Department b
     on a.DepartmentId = b.Id
  where a.rank <= 3
```

우선 해당 데이터를 뽑기위해 해당 row의 rank를 구하는 변수인 @curRank, 해당 row 의 DepartmentId의 전 row의  DepartmentId를 임시로 저장하는 @temp_dept, 해당 row 의 salary의 전 row의  salary의 임시로 저장하는 @temp_sal 변수를 선언해 주었다.

그 이후 order by를 통해  DepartmentId 오름차순, Salary 내림차순을 통해 정렬을 시켰다. 

한 row가 돌아갈때마다 case문을 통해 해당 row의 DepartmentId가 전 row의 DepartmentId와 같을 경우 해당 row의 Salary가 전 Row의 Salary가 같은지 한 번더 비교 후 같으면 rank고정 다르면 rank + 1을 통해 rank를 증가시켜주었다.

마지막으로 해당 쿼리로 뽑힌 데이터들 중에 rank가 3이하인 데이터만 뽑고 Department 테이블과 inner join을 통해 원하는 데이터들을 도출 하였다.

### 🧐 후기

사용자 정의 변수를 사용하고 여러번의 쿼리 도출로 쿼리의 기독성이 떨어져서 고민중에 leetcode의 solution 코드를 확인 하였다.

```mysq
SELECT
    d.Name AS 'Department', e1.Name AS 'Employee', e1.Salary
FROM
    Employee e1
        JOIN
    Department d ON e1.DepartmentId = d.Id
WHERE
    3 > (SELECT
            COUNT(DISTINCT e2.Salary)
        FROM
            Employee e2
        WHERE
            e2.Salary > e1.Salary
                AND e1.DepartmentId = e2.DepartmentId
        )
;
```

solution코드를 보니 매우 간결하였다. 우선 salary의 top3 라는건 자기자신보다 salary가 큰 사람이 3명 미만이라는 소리와 같다. 

그렇기 때문에 WHERE절의 코드는 위와 같다. 메인 쿼리의 e1 과 서브 쿼리의 e2의 DepartmentId가 서로 같으며 e1 의 salary보다 큰 e2의 salary를 가진 사람이 3명 이하여야 한다는 조건 문이다.

이후, 나머지는 Department Name을 가져오기 위해 Department와 Join하는 쿼리이다.

Solution 쿼리를 보고 난후, 문제에 대해 발상의 전환을 통해 좀더 쿼리를 쉽게 뽑아오는 연습을 해야겠다는 생각이 들었다.