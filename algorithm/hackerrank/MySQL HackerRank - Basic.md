[문제링크](https://www.hackerrank.com/domains/sql?filters%5Bskills%5D%5B%5D=SQL%20%28Basic%29)


## Revising the Select Query I
---
```sql
select * from city 
where population>100000 and countrycode = 'usa';
```
<Br>

## Revising the Select Query II
---
```sql
select name from city 
where population >120000 and countrycode = 'usa';
```
<Br>

## Select All
---
```sql
select * from city;
```
<Br>

## Select By ID
---
```sql
select * from city where id = 1661;
```
<Br>

## Japanese Cities' Attributes
---
```sql
select * from city where countrycode ='jpn';
```
<Br>

## Japanese Cities' Names
---
```sql
select name from city where countrycode ='jpn';
```
<Br>

## Weather Observation Station 1
---
```sql
select city,state from station;
```
<Br>

## Weather Observation Station 2
---
```sql
select round(sum(lat_n),2),round(sum(long_w),2)
from station;
```
+ round(숫자, 소수점자리) : 위 코드에서 보면 소수 2째자리부터 반올림 ->1.235-> 1.24

## Weather Observation Station 3
---
```sql
select distinct city from station where id%2=0;
```
<Br>

## Weather Observation Station 4
---
```sql
select count(*) - count(distinct city) from station;
```
<Br>

## Weather Observation Station 6
---
```sql
-- 방법 1
select city from station 
where city like "a%" or city like "e%" or city like "i%" or city like "o%" or city like "u%";

-- 방법 2
select city 
from station 
where city regexp '^[aeiou]'
```
regexp '^[aeiou]' : aeiou로 시작하는 문자열 찾기  
^은 시작, $은 끝
<Br>

## Weather Observation Station 7
---
```sql
-- 방법 1
select distinct city from station 
where city like "%a" or city like "%e" or city like "%i" or city like "%o" or city like "%u";

-- 방법 2
SELECT distinct city 
FROM station
WHERE city REGEXP '[aeiou]$' 
```
^은 시작, $은 끝
<Br>

## Weather Observation Station 8
---
```sql
-- 방법 1
SELECT distinct city 
FROM station
WHERE city REGEXP '[aeiou]$' and city REGEXP '^[aeiou]';

-- 방법 2
-- 설명은 12번 참고
select distinct city from station 
where city regexp '^[aeiou].*[aeiou]$'
```
^와 $를 같이 사용하면 오류가 뜬다. and로 따로 해줘야 한다. 정규식에서 |는 있는데 &는 없는 것 같다.
<Br>

## Weather Observation Station 9
---
```sql
select distinct city 
from station 
where city regexp '^[^aeiou]';
```
[] 안의 ^는 aeiou를 제외한다는 뜻
<Br>

## Weather Observation Station 10
---
```sql
select distinct city 
from station 
where city regexp '[^aeiou]$';
```
<Br>

## Weather Observation Station 11
---
```sql
-- 방법 1
select distinct city 
from station 
where city regexp '^[^aeiou]|[^aeiou]$';

-- 방법 2
select distinct city from station 
where city regexp '^[^aeiou]'
or city regexp '[^aeiou]$'
```
| -> or 을 의미하고 주의할 점은 |양쪽에 공백을 주면 안된다. 그리고 ''안에 한번에 작성해야 한다.  
|을 사용하지 않고 or로 두개를 나눠서 사용해도 된다.

<Br>

## Weather Observation Station 12
---
```sql
-- 방법 1
select distinct city
from station
where city regexp '^[^aeiou].*[^aeiou]$';

-- 방법 2
select distinct city 
from station 
where city regexp '^[^aeiou]'
and city regexp'[^aeiou]$';
```
+ .은 아무런 문자 하나를 의미한다. ...는 아무런 문자 3개를 의미한다.  
+ *는 바로 앞의 문자가 0회 이상 나타나는 문자를 찾는다.

즉, aeiou가 맨 앞글자가 아니고 사이에는 어떠한 문자가 0회이상 나타나고 끝에는 aeiou가 아닌 문자열 찾기가 된다.
<Br>

## Weather Observation Station 13
---
```sql
select truncate(sum(lat_n),4)
from station
where lat_n> 38.7880 and lat_n<137.2345;
```
+ truncate(숫자,버릴자리수) : 버릴 자리수가 4면 38.78805 -> 38.7880

## Weather Observation Station 14
---
```sql
select truncate(max(lat_n),4)
from station
where lat_n<137.2345;
```

## Weather Observation Station 15
---
```sql
select round(long_w,4)
from station
where lat_n <137.2345
order by lat_n desc
limit 1;
```

## Weather Observation Station 16
---
```sql
select round(lat_n,4)
from station
where lat_n>38.7780
order by lat_n
limit 1;
```
## Weather Observation Station 17
---
```sql
select round(long_w,4)
from station
where lat_n >38.7780
order by lat_n
limit 1;
```
## Weather Observation Station 18
---
```sql
-- 방법 1
select round(max(lat_n)-min(lat_n) + max(long_w)-min(long_w),4)
from station;

-- 방법 2
set @a = (select lat_n from station order by lat_n limit 1);
set @b = (select long_w from station order by long_w limit 1);
set @c = (select lat_n from station order by lat_n desc limit 1);
set @d = (select long_w from station order by long_w desc limit 1);

select round(abs(@a-@c) + abs(@b-@d),4);
```
서브쿼리는 ; 사용하면 오류뜬다.

## Weather Observation Station 19
---
```sql
select round(
    sqrt(
        pow(max(lat_n)-min(lat_n),2)
        +pow(max(long_w)-min(long_w),2)
    )
    ,4)
from station;
```
+ pow(수,지수승) : pow(2,3) = 2 * 2 * 2
+ sqrt : 루트

## Higher Than 75 Marks
---
```sql
select name from students 
where marks >75 order by right(name,3),id;
```
+ right(문자열,가져올 개수)
+ mid(문자,시작위치,가져올 개수)
+ left(문자,가져올 개수)

주의해야할 것이 mysql은 0부터시작이 아니고 1부터 시작이다.
<Br>

## Employee Names
---
```sql
select name from employee order by name;
```
<Br>

## Employee Salaries
---
```sql
select name from employee
where salary>2000 and months<10 
order by employee_id;
```
<Br>

## Type of Triangle
---
```sql
select 
case
  when a=b and b=c then 'Equilateral'
  when a>=b+c or b>=a+c or c>=a+b then 'Not A Triangle'
  when a=b or b=c or a=c then 'Isosceles'
  else 'Scalene'
end
from TRIANGLES;
```
<Br>


## The PADS
---
```sql
select concat(name,'(',substr(occupation,1,1),')')
from occupations 
order by name;

select concat('There are a total of ',count(*),' ', lower(occupation),'s.')
from occupations
group by occupation
order by count(*),occupation;
```
+ concat : 쉼표를 구분으로 문자열을 엮어준다.
+ substr(문자열,시작점,개수) : 시작점부터 개수만큼 잘라서 반환
+ lower(문자열) : 소문자로 반환
+ upper(문자열) : 대문자로 반환
+ 쿼리 두 개 이상일 경우 반드시 쿼리마다 세미콜론 ; 붙이기 -> 안붙이면 오류 발생
<Br>


## Revising Aggregations - The Count Function
---
```sql
select count(*) from city where population>100000;
```
<Br>

## Revising Aggregations - The Sum Function
---
```sql
select sum(population)
from city
where district ='california';
```
<Br>

## Revising Aggregations - Averages
---
```sql
select avg(population)
from city
where district='california';
```
<Br>

## Average Population
---
```sql
select floor(avg(population))
from city;
```
+ ceil : 올림, ceiling이랑 똑같음
+ floor : 내림
+ round : 반올림 -> floor, ceil과 다르게 소수점 파라미터 존재
<Br>

## Japan Population
---
```sql
select sum(population)
from city
where countrycode ='jpn';
```
<Br>

## Population Density Difference
---
```sql
select max(population)-min(population)
from city;
```
<Br>

## The Blunder
---
```sql
select ceil(avg(salary) - avg(replace(salary,'0','')))
from employees;
```
replace가 숫자도 바꿔줄 수 있다.('0' -> 0 으로 해봤는데도 정상 작동)
<Br>

## Top Earners
---
```sql
-- 방법 1
select salary*months as earnings ,count(*)
from employee
group by earnings
order by earnings desc
limit 1;

-- 방법 2
-- where조건에 집계함수 못쓰므로 서브쿼리로 작성
select max(salary*months) ,count(*)
from employee
where salary*months = (select max(salary*months) from employee)
```
<Br>

## Asian Population
---
```sql
select sum(a.population)
    from city a
    inner join country b
    on a.countrycode = b.code
    where b.continent = 'Asia';
```
<Br>

## African Cities
---
```sql
select a.name
    from city a
    inner join country b
    on a.countrycode = b.code
    where continent='Africa';
```
<Br>

## Average Population of Each Continent
---
```sql
select b.continent, floor(avg(a.population))
    from city a
    inner join country b
    on a.countrycode = b.code
    group by b.continent;
```


