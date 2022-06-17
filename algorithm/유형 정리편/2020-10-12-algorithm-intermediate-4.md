---
layout: post
title:  정렬 기출문제
subtitle:   정렬 기출문제
categories: algorithm
tags: algorithm-intermediate
comments: true
# header-img:
---
* 
{:toc}

## 1. 간단 정리
---
정렬은 데이터를 특정한 기준에 따라서 정렬하기 위해 사용하는 알고리즘이다. 대표적인 정렬 라이브러리를 성능에 따라서 비교하는 다음과 같다.

정렬 알고리즘|평균 시간 복잡도|공간 복잡도|특징
---|---|---|---|---
선택 정렬|O(N^2)|O(N)|아이디어가 매우 간단
삽입 정렬|O(N^2)|O(N)|데이터가 거의 정렬되어 있을 때는 가장 빠름
퀵 정렬|O(NlogN)|O(N)|대부분의 경우에 가장 적합하며, 충분히 빠름
계수 정렬|O(N+K),(K는 데이터 중 가장 큰 양수)|O(N+K),(K는 데이터 중 가장 큰 양수)|데이터의 크기가 한정되어 있는 경우에만 사용 가능, 매우 빠름

또한 각 정렬 알고리즘의 동작 아이디어를 한 문장으로 정리하면 다음과 같다.

정렬 알고리즘|핵심 아이디어
---|---
선택 정렬|가장 작은 데이터를 선택해서 정렬되지 않은 데이터 중에서 가장 앞쪽에 있는 데이터와 위치를 바꾸는 방법
삽입 정렬|데이터를 앞에서부터 하나씩 확인하며 데이터를 적절한 위치에 삽입하는 방법
퀵 정렬|기준 데이터를 설정하고 그 기준보다 큰 데이터와 작은 데이터의 위치를 바꾸는 방법
계수 정렬|특정한 값을 가지는 데이터의 개수를 카운트 하는 방법

파이썬의 표준 라이브러리에서 기본으로 제공하는 정렬 라이브러리는 최악의 경우에도 시간 복잡도 O(NlogN)을 보장한다. 따라서 계수 정렬을 사용해 매우 빠르게 정렬해야 하는 특이한 케이스가 아니라면 파이썬의 정렬 라이브러리를 사용하는 것이 가장 합리적이다. 정렬은 다양한 알고리즘에서 사용되는데, 대표적으로 이진 탐색의 경우 데이터가 정렬되어 있을 때만 사용할 수 있다. 크루스칼 알고리즘의 경우, 간선의 정보를 정렬하는 과정이 반드시 필요하다. 
<br>

## 2. 국영수
---
[문제 클릭](https://www.acmicpc.net/problem/10825){: target="_blank"}  

### 내가 작성한 코드
```python
n = int(input())
table = []

for _ in range(n):
    table.append(input().split())

table.sort(key = lambda x:(-int(x[1]),int(x[2]),-int(x[3]),x[0]))

for i in range(n):
    print(table[i][0])
```
파이썬의 정렬 내장함수는 최악의 경우에도 NlogN을 보장하기 때문에 주어진 범위 내에서 충분히 사용할 수 있다.



<br>

## 3. 안테나
---
[문제 클릭](https://www.acmicpc.net/problem/18310){: target="_blank"}  

### 내가 작성한 코드
```python
n = int(input()) # 집의수
table = list(map(int,input().split())) # 집의 위치
table.sort() # 정렬
print(table[(n-1)//2]) # 정렬후 가장 가운데 있는 곳에 설치해야 최소
```
범위가 200,000만 이므로 적어도 선형 로그 시간 알고리즘으로 설계해야한다. 따라서 각각의 위치에 설치하고 일일이 비교하는 설계는 시간초과가 발생할 것이다. 내장함수를 이용해서 정렬하고 결국 집들의 가운데 있는 집에 설치하는 것이 최소거리를 만족할 것이므로 집들 중에서 가운데 있는 곳에 설치하면 된다. 홀수는 상관없으나 짝수의 경우 인덱스때문에 -1을 해주고 나눗셈을 해줘야 제일 먼저 나오는 최소거리 집의 위치가 된다.

<br>

## 4. 실패율
---
[문제 클릭](https://programmers.co.kr/learn/courses/30/lessons/42889){: target="_blank"}  

### 내가 작성한 코드
```python
from bisect import bisect_left, bisect_right

def solution(N, stages):
    stages.sort()
    people = len(stages)
    result = []
    fail = []
    for i in range(1, N + 1):
        cnt = bisect_right(stages, i) - bisect_left(stages, i)
        if cnt == 0:
            percent = 0
        else:
            percent = cnt / people
        fail.append((percent, i))
        people -= cnt

    fail.sort(key=lambda x: (-x[0], x[1]))

    for percent, idx in fail:
        result.append(idx)

    return result
```


### 모범답안
```python
def solution(N, stages):
    answer = []
    length = len(stages)

    # 스테이지 번호를 1부터 N까지 증가시키며
    for i in range(1, N + 1):
        # 해당 스테이지에 머물러 있는 사람의 수 계산
        count = stages.count(i)
        
        # 실패율 계산
        if count == 0:
            fail = 0
        else:
            fail = count / length
        
        # 리스트에 (스테이지 번호, 실패율) 원소 삽입
        answer.append((i, fail))
        length -= count

    # 실패율을 기준으로 각 스테이지를 내림차순 정렬
    answer = sorted(answer, key=lambda t: t[1], reverse=True)
    # 애초에 스테이지 번호가 작은 순으로 저장되었기때문에 기준으로 정렬한 뒤에는
    # 원래 있었던 순으로 정렬되므로 따로 스테이지 번호순 정렬을 할 필요가 없다.
    
    # 정렬된 스테이지 번호 반환
    answer = [i[0] for i in answer]
    return answer
```


<br>

## 5. 카드 정렬하기
---
[문제 클릭](https://www.acmicpc.net/problem/1715){: target="_blank"}  

### 내가 작성한 코드
```python
import heapq

n = int(input())
q = []
ans = 0
for _ in range(n):
    heapq.heappush(q, int(input()))

while len(q) != 1:
    tmp = heapq.heappop(q) + heapq.heappop(q)
    ans += tmp
    heapq.heappush(q, tmp)

print(ans)
```



  

---
__본 포스팅은 '이것이 코딩 테스트다 with 파이썬'을 읽고 공부한 내용을 바탕으로 작성하였습니다.__
