[문제 링크](https://programmers.co.kr/learn/challenges?tab=all_challenges)

## 1. 우유와 요거트가 담긴 장바구니
---
```sql
-- 방법 1
SELECT a.cart_id 
    from (select cart_id from cart_products where name = 'Milk') a
    inner join
    (select cart_id from cart_products where name = 'Yogurt') b
    on a.cart_id = b.cart_id;

-- 방법 2
select a.cart_id
    from cart_products a
    inner join cart_products b
    on a.cart_id = b.cart_id    
    where a.name ='Milk' and b.name ='Yogurt'
    group by a.cart_id    

-- 방법 3
select distinct a.cart_id
    from cart_products a
    inner join cart_products b
    on a.cart_id = b.cart_id 
    where a.name = 'Milk' and b.name = 'Yogurt'
```

<br>

## 2. 입양 시각 구하기2
---
```sql
set @hour =-1;
select 
    (@hour := @hour+1) hour,
    (select count(*) from animal_outs where hour(datetime)=@hour) count
from animal_outs
where @hour<23;
```
__반드시 변수 선언 후에 ; 세미콜론을 붙여줘야한다.__  
변수의 증가를 이용해서 where 조건을 만족하면 계속 select한다. 마치 for문과 비슷하다.  
hour<23 으로 설정해야 22가 들어가서 23이 만들어지고 종료된다.  
전에 풀었던 입양 시각 구하기1 문제처럼 코딩한다면 있는 시간만 조회하므로 0~23까지 중에서 시간 중에서 hour(datetime)으로 만들어지지 않는 시간의 경우는 조회 행에 출력되지 않기 때문에 위처럼 코딩해야한다.
<br>

## 3. 보호소에서 중성화한 동물
---
```sql
SELECT ins.animal_id,ins.animal_type,ins.name
    from animal_ins ins
    inner join animal_outs outs
    on ins.animal_id = outs.animal_id
    where ins.SEX_UPON_INTAKE like "Intact%" and outs.SEX_UPON_OUTCOME not like "Intact%";
```
<br>

