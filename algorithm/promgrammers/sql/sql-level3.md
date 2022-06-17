[문제 링크](https://programmers.co.kr/learn/challenges?tab=all_challenges)


## 1. 없어진 기록 찾기
---
```sql
SELECT outs.animal_id, outs.name 
    from animal_ins ins
    right join animal_outs outs
    on outs.animal_id = ins.animal_id
    where ins.animal_id is null;    
```
outer join으로 id가 같은 것 + outs의 모든 것이 조회된다. outs에만 있고 ins의 없는 경우 outs의 아이디만 적히고 ins의 아이디는 null로 표현되는데 이것을 조건으로 사용하면 된다.

<br>

## 2. 있는데요 없었습니다
---
```sql
SELECT ins.animal_id,ins.name
    from animal_ins ins
    inner join animal_outs outs
    on ins.animal_id = outs.animal_id
    where ins.datetime>outs.datetime
    order by ins.datetime;
```

<br>

## 3. 오랜 기간 보호한 동물1
```sql
SELECT ins.name,ins.datetime
    from animal_ins ins
    left join animal_outs outs
    on ins.animal_id = outs.animal_id
    where outs.animal_id is null
    order by ins.datetime
    limit 3;
```

<br>

## 4. 오랜 기간 보호한 동물2
```sql
-- 방법 1
SELECT outs.animal_id, outs.name
    from animal_ins ins
    inner join animal_outs outs
    on ins.animal_id = outs.animal_id
    order by outs.datetime - ins.datetime desc
    limit 2;

-- 방법 2
SELECT outs.animal_id, outs.name
    from animal_ins ins
    inner join animal_outs outs
    on ins.animal_id = outs.animal_id
    order by datediff(outs.datetime,ins.datetime) desc
    limit 2;
```
+ datediff(날짜1,날짜2) : 날짜1 - 날짜2의 일수를 결과로 반환
+ timediff(시간1,시간2) : 시간1 - 시간2의 시간차 결과를 반환
    - 해당 문제에서는 timediff를 사용하면 max값을 초과해버려서 사용 불가능
+ timestampdiff(단위,날짜1,날짜2) : 단위 표현에 따른 결과 반환
    - 단위 : second,minute, hour, day, week, month, quarter, year

## 5. 헤비 유저가 소유한 장소
서브 쿼리 보다는 join이 훨씬 좋다는 것은 자명한 사실이다.  
이상적으로 생각하면 서브 쿼리가 먼저 실행되고 바깥 sql문이 실행된다고 생각하겠지만 실제로는 바깥쿼리문이 먼저 실행되기 때문에 서브 쿼리는 계속해서 실행된다.  
하지만 이 문제는 조건에 따라 한번 걸러내야 하므로 서브 쿼리를 사용할 수 밖에 없다.  
```sql
select id,name,host_id 
from places
where host_id in (select host_id from places group by host_id having count(*)>=2)
```
1차적 풀이이다.  
서브 쿼리는 어쩔수 없이 사용한다 치고, 서브쿼리에서 in절은 최악이다.  
in은 결국 =과 같아서 in의 서브쿼리로 나온 결과물을 하나씩 비교한다.  
<br>

```sql
select * from places p1
where exists ( 
    select 1 from places p2 
     where p1.host_id = p2.host_id 
     group by host_id 
     having count(host_id)>=2
)
```
exists는 서브 쿼리 안에 결과값이 1개라도 있으면 더이상 수행하지 않는다.  
따라서 in보다 성능이 더 좋다.  
select 절에 1은 더미값으로 해당 서브 쿼리 결과물이 존재한다고 찍어주는 값에 불과하다.  
하지만 이도 서브 쿼리가 들어가기 때문에 바깥 쿼리가 먼저 실행되고 안쪽 쿼리는 반복되서 실행된다는 점을 기억하자.  