[문제 링크](https://programmers.co.kr/learn/challenges?tab=all_challenges)

## 1. 최댓값 구하기
---
```sql
SELECT datetime as '시간' from animal_ins order by datetime desc limit 1
```
<br>


## 2. 모든 레코드 조회하기
---
```sql
SELECT * from animal_ins;
```
<br>

## 3. 역순 정렬하기
---
```sql
SELECT name, datetime from animal_ins order by animal_id desc;
```
<br>

## 4. 아픈 동물 찾기
---
```sql
SELECT animal_id, name from animal_ins where INTAKE_CONDITION = 'sick' order by animal_id ;
```
<br>

## 5. 어린 동물 찾기
---
```sql
-- 방법 1
select animal_id,name from animal_ins 
where not intake_condition in ('aged')
order by animal_id;

-- 방법 2
select animal_id,name from animal_ins 
where intake_condition != 'aged'
order by animal_id;

-- 방법 3
select animal_id,name from animal_ins 
where intake_condition <> 'aged'
order by animal_id;
```
!= 는 <>로 자동 변환되어 사용되므로 퍼포먼스를 위해 <>를 사용하는 것이 좋다.

<br>

## 6. 동물의 아이디와 이름
---
```sql
SELECT animal_id,name from animal_ins order by animal_id;
```
<br>

## 7. 이름이 없는 동물의 아이디
---
```sql
SELECT animal_id from animal_ins where name is null;
```
where 문에서 null 확인은 is 사용
<br>

## 8. 여러 기준으로 정렬하기
---
```sql
select animal_id,name,datetime from animal_ins order by name, datetime desc;
```
<br>

## 9. 상위 n개 레코드
---
```sql
SELECT name from animal_ins order by datetime limit 1;
```
<br>

## 10. 이름이 있는 동물의 아이디
---
```sql
SELECT animal_id from animal_ins where name is not null order by animal_id;
```
pk가 id라면 자동으로 오름차순 정렬되긴 해서 따로 정렬 안해도 된다.
<br>




