[문제링크](https://www.hackerrank.com/domains/sql?filters%5Bskills%5D%5B%5D=SQL%20%28Intermediate%29)

## Weather Observation Station 5
---
```sql
-- 방법 1
select city,char_length(city) 
  from station 
  order by char_length(city), city 
  limit 1;
select city,char_length(city) 
  from station 
  order by char_length(city) desc, city
  limit 1;

-- 방법 2
(select city,char_length(city) 
from station 
order by char_length(city), city 
limit 1)
union
(select city,char_length(city) 
from station
order by char_length(city) desc, city
limit 1);
```
union은 결과를 합쳐서 중복을 제거하고 출력해주고 열이름은 1번째 것을 따른다. union all은 중복을 포함해서 출력해준다.  
영어를 사용할 때는 length()를 사용해도 무관하나, 한글일 경우 char_length를 사용해야 한다.  
length를 사용해서 '안녕'을 입력해보면 결과값이 6으로 나온다.
<Br>


## Binary Tree Nodes
---
```sql
-- 방법 1
select n,case
    when p is null then 'Root'
    when n in (select distinct p from bst) then 'Inner'
    else 'Leaf'
    End
    from bst
    order by n;

-- 방법 2
select n, case
            when p is null then 'Root'
            when exists (select 1 from bst b2 where b2.p=b1.n) then 'Inner'
            else 'Leaf'
        end
from bst b1
order by n
```
in보다는 exists가 성능상 좋다.

<br>

## New Companies
---
```sql
--- 방법 1
select c.company_code, c.founder,
    count(distinct(l.lead_manager_code)),
    count(distinct(s.senior_manager_code)),
    count(distinct(m.manager_code)),
    count(distinct(e.employee_code))
from company c
join lead_manager l on c.company_code = l.company_code
join senior_manager s on s.company_code = l.company_code
join manager m on m.company_code = s.company_code
join employee e on e.company_code = m.company_code
group by c.company_code,c.founder
order by company_code



--- 방법 2
select c.company_code,c.founder,
    count(distinct l.lead_manager_code),
    count(distinct s.senior_manager_code), 
    count(distinct m.manager_code),
    count(distinct e.employee_code)
    from company c, lead_manager l,senior_manager s,manager m,employee e
    where c.company_code=l.company_code and 
    l.company_code=s.company_code and 
    s.company_code=m.company_code and 
    m.company_code=e.company_code
    group by c.company_code,c.founder
    order by c.company_code    
```
+ c.founder을 group by에 포함시키지 않으니 오류가 뜬다. company_code로만 group by시키면 만약 c.founder에 여러 인물이 있을 수 있으니 선택하지 못해 오류가 뜨는 것 같다. 따라서 group by를 사용하고 열을 select할 때는 열에 특별한 작업(함수)을 하지 않았다면 group by에서 사용한 열만 select 할 수 있다.
+ inner join은 각각 join하지 않고 from으로 한 번에 작성해서 on 대신 where로 사용하면 된다.
<br>

## Symmetric Pairs
---
```sql
select a.x,a.y
    from functions a
    inner join functions b
    on a.x = b.y and b.x=a.y    -- on 에서 이어진 조건은 ,가 아니라 and 사용
    group by a.x,a.y
    having count(*)>1 or a.x<a.y
    order by a.x
```
+ on 조건에 맞도록 테이블이 조회되고 a.x,a.y로 묶으면 where 조건으로 a.x<=a.y 넣어주면 끝날 줄 알았다. 하지만 중복에서 문제가 있다. 만약 20,20이 한 번만 있다면 문제 상 이것이 2개가 있어야 symmetric이다. where조건만으로 끝내버리면 20,20이 한번만 있어도 출력된다. 따라서 다른 조건이 필요하다. x<=y 형식으로 출력해야하므로 x < y 조건과 x = y인 조건을 따로 만드는 것이 해결책이다. x = y인 경우는 a.x,a.y로 그룹핑된 열 카운트가 1개보다 많으면 같은 x = y가 2개 이상 있다는 의미로 1개만 있는 경우를 제외시킬 수 있다. 이외에는 on과 group의 조건으로 잘 만들어진 상태이므로 x < y로 처리하면 된다.
<br>

## Weather Observation Station 20

---
```sql
set @n =0;
select count(*) from station into @total;

select round(avg(a.lat_n),4)
    from (select @n:=@n+1 as row_id,lat_n from station order by lat_n) a
    where case
        when @total%2=0 then a.row_id in (@total/2, (@total/2+1))
        else a.row_id = (@total+1)/2
        end;
```
<br>

## SQL Project Planning
---
```sql
select start_Date, min(end_date)
from
(select start_date from projects where start_date not in (select end_date from projects)) as a
 inner join 
(select end_Date from projects where end_Date not in (select start_date from projects)) as b
 on start_Date < end_Date
 group by start_Date
 order by datediff(min(end_Date),start_Date), start_Date;
```
프로젝트 단위에서 시작일과 종료일만 뽑아서 join한 뒤 start < end 로 쌍을 만들어서 start로 그루핑해준다. 그러면 그루핑되어 딸려온 end는 전부 프로젝트의 종료일인데 여기서 제일 빠른 종료일이 해당 프로젝트의 종료일이 된다.
<br>

## Placements
---
```sql
select s.name
    from students s
    join packages p1 on s.id = p1.id
    join friends f on p1.id = f.id
    join packages p2 on f.friend_id = p2.id
    where p2.salary - p1.salary>0
    order by p2.salary;
```
<br>

## The Report
---
```sql
select name,grade,marks
from  students s
    join grades g
    on s.marks between g.min_mark and g.max_mark
    where grade>=8
order by grade desc, name;

select if(grade<8,null,name),grade,marks
from  students s
    join grades g
    on s.marks between g.min_mark and g.max_mark
    where grade<8
order by grade desc, marks;
```
on의 조건으로 between and를 사용할 수 있다.

<br>

## Top Competitors
---
```sql
-- 방법1
select h.hacker_id, h.name
    from hackers h
    join submissions s on h.hacker_id = s.hacker_id
    join challenges c on s.challenge_id = c.challenge_id
    join difficulty d on c.difficulty_level = d.difficulty_level     
    where d.score = s.score
    group by h.hacker_id,h.name
    having count(*)>1
    order by count(*) desc,h.hacker_id;        

-- 방법2
select h.hacker_id, h.name
    from hackers h, difficulty d, challenges c, submissions s
    where h.hacker_id = s.hacker_id
    and s.challenge_id = c.challenge_id
    and c.difficulty_level = d.difficulty_level
    and d.score = s.score
    group by h.hacker_id,h.name
    having count(*)>1
    order by count(*) desc,h.hacker_id;        
```
<br>

## Ollivander's Inventory
---
```sql
select w2.id,p.age,w1.coins, w1.power
from (select code, min(coins_needed) coins, power from wands group by code,power) w1
join wands w2
on w1.code = w2.code and w1.coins = w2.coins_needed and w1.power = w2.power
join wands_property p
on p.code = w2.code
where p.is_evil = 0
order by power desc, age desc
```
코드별로 파워가 가장 큰 것중에 비용이 가장 작은 것을 뽑아내야 한다.  
이를 뽑아내기 위해서는 group by로 code와 power를 묶어야하는데 출력값에 id가 필요하다.  
하지만 group by로 id까지 묶으면 정상적으로 group by가 되지 않는다.  
따라서 분리해서 우선 id를 제외하고 뽑은 뒤에 조인으로 id값을 찾아내야 한다.  

<br>

## Challenges
---
```sql
--- 방법 1
select h.hacker_id,h.name,count(*) cnt
from hackers h
join challenges c
on h.hacker_id = c.hacker_id
group by h.hacker_id, h.name
having cnt = (select count(*) 
              from challenges c 
              group by hacker_id 
              order by count(*) desc 
              limit 1
             )
        or
        cnt in (select t.cnt 
                from (select count(*) cnt 
                      from challenges c 
                      group by hacker_id) t
                group by t.cnt 
                having count(*)=1
               )
order by cnt desc, hacker_id

--- 방법 2
select h.hacker_id, h.name, count(h.hacker_id) cnt
    from hackers h
    join challenges c
    on h.hacker_id = c.hacker_id
    group by h.hacker_id,h.name
    having cnt = (select max(t.cnt) from 
        (select count(*) cnt from challenges group by hacker_id) t)
    or
        cnt in (select p.cnt from
        (select count(*) cnt from challenges group by hacker_id) p
        group by p.cnt
        having count(p.cnt)=1)
    
    order by cnt desc, h.hacker_id;

```
집계함수는 max(count(*))처럼 중첩해서 쓸 수 없다.  
사용하기 위해서는 먼저 count(*)를 꺼내오고 그 후에 max를 사용할 수 있다.  


<br>

## Contest Leaderboard
---
```sql
select h.hacker_id,h.name, sum(t.score) score
from (select hacker_id, max(score) score from submissions group by hacker_id,challenge_id) t
join hackers h
on h.hacker_id = t.hacker_id
group by h.hacker_id,h.name
having score >0
order by score desc, hacker_id
```
서브 쿼리로 사람마다 각 문제에 대해 최고점수를 뽑아내고 그것을 id 기준으로 조인하고 group하면 각 문제에 대한 최고 점수를 가지고 있으니 그것을 sum하면 된다.


<br>


## Interviews
---
```sql
select con.contest_id,
        con.hacker_id, 
        con.name, 
        sum(total_submissions), 
        sum(total_accepted_submissions), 
        sum(total_views),
        sum(total_unique_views)
from contests con 
join colleges col on con.contest_id = col.contest_id 
join challenges cha on  col.college_id = cha.college_id 
left join
(select challenge_id, sum(total_views) as total_views, sum(total_unique_views) as total_unique_views
from view_stats group by challenge_id) vs on cha.challenge_id = vs.challenge_id 
left join
(select challenge_id, sum(total_submissions) as total_submissions, sum(total_accepted_submissions) as total_accepted_submissions from submission_stats group by challenge_id) ss on cha.challenge_id = ss.challenge_id
    group by con.contest_id, con.hacker_id, con.name
        having sum(total_submissions)!=0 or 
                sum(total_accepted_submissions)!=0 or
                sum(total_views)!=0 or
                sum(total_unique_views)!=0
            order by contest_id;
```
위에는 무난한 join이고 아래서 left join을 하는 이유는 college에서 선택된 challenge만 필요하기 때문이다. 그리고 하나라도 0이 아니면 총 합이 0이 아니므로 having의 조건으로 사용했다.

<br>

## 정리
프로그래머스와 Hackers의 sql을 풀면서 기억해야할 사항을 정리하려고 한다.
+ MySQL은 인덱스가 1부터 시작한다.
+ where문에서는 집계함수를 사용할 수 없다.
+ having문은 group by와 함께 쓰여야 한다.
+ select 절의 별칭은 order by, group by, having 에서만 사용 가능하다.
+ regexp 정규식 사용법을 익히자.
    - or의 경우 |를 사용할 수 있지만, and의 경우 &는 없다.
+ 문자열 가져오기
    - right(문자열, 개수) : 오른쪽에서 개수만큼 문자열 가져오기
    - left(문자열, 개수) : 왼쪽에서 개수만큼 문자열가져오기
    - mid(문자열, 시작인덱스, 가져올 개수) : 시작 인덱스부터 가져올 개수만큼 문자열을 가져오기
+ Case문은 Case when then end로 끝난다.
+ 대소문자 변환은 lower(), upper()을 사용한다.
+ concat() 은 문자열을 이어 붙일 때 사용ㅎ나다.
+ substr(문자열, 시작인덱스, 가져올 개수), substring(문자열, 시작인덱스, 가져올 개수) : 문자열을 시작 인덱스부터 개수만큼 잘라서 가져온다. 인덱스는 1부터 시작이니 주의할 것
+ floor()는 내림, ceil()는 올림, round(숫자,소숫점자리수)는 반올림, truncate(숫자,소수점자리수)는 내림이다.
    - 소수점 자리수를 음수로 두면 1의자리부터 시작된다. -> -1는 1의자리
+ replace(문자열,대상,변환)은 문자열을 교체해준다.
+ date_format(인자,'형식')으로 date의 형식을 바꿀 수 있다.
+ null 처리는 is null, is not null로 한다.
+ 변수를 사용해서 루프를 주는 경우 where문이 for문의 역할을 한다.
+ select 절에 집계함수를 중첩해서 사용 불가능 ex) max(count(*)) -> 서브쿼리로 count를 우선 빼와서 사용해야 한다.