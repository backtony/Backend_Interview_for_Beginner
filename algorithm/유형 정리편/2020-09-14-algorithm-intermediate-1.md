---
layout: post
title:  그리디 기출문제
subtitle:   그리디 기출문제
categories: algorithm
tags: algorithm-intermediate
comments: true
# header-img:
---
* 
{:toc}


## 1. 그리디란?
---
현재 상황에서 가장 좋아보이는 것만 선택하는 알고리즘이다. 코딩 테스트에서는 대부분 최적의 해를 찾는 문제가 출제되기 때문에 그리디 알고리즘의 정당성을 고민하면서 문제 해결 방안을 생각해야 한다. 대표적인 예시로는 거스름돈 문제와 1이 될 때까지 1빼기 혹은 K나누기 연산의 최소값 문제가 있다. 그리디 유형의 문제 특징은 다양한 알고리즘에서 사용되고 있다는 점인데 다익스트라 최단 경로 알고리즘과 크루스칼 알고리즘은 모두 그리디 알고리즘에 속한다.  
<br>

## 2. 모험가 길드
---
한 마을에 모험가가 N명이 있고 모험가를 대상으로 공포도를 측정했다. 공포도가 X인 모험가는 반드시 X명 이상으로 구성한 모험가 그룹에 참여해야 여행을 떠날 수 있다는 규정이 있다. 길드장은 최대 몇 개의 모험가 그룹을 만들 수 있는지 궁금해한다. 길드장을 위해 N명의 모험가에 대한 정보가 주어졌을 때, 여행을 떠날 수 있는 그룹 수의 최대값을 구하는 프로그램을 작성하시오. 단, 몇 명의 모험가는 마을에 그대로 남아 있어도 되기 때문에, 모든 모험가를 특정한 그룹에 넣을 필요는 없다.  
__입력 조건__  
+ 첫째 줄에 모험가의 수가 주어진다. (1<=N<=100,000)
+ 둘째 줄에 각 모험가의 공포도의 값을 N이하의 자연수로 주어지며 공백으로 구분한다.

__출력 조건__  
+ 여행을 떠날 수 있는 그룹의 최대 수를 출력한다.

```
입력예시
5
2 3 1 2 2

출력 예시
2
```

### 내가 작성한 코드
```python
# 아이디어
# 가장 많은 그룹을 만들어야함 -> 공포지수가 가장 적은 사람들끼리 우선적으로 묶으면 가장 많이 만들 수 있겠다.

import sys

input = sys.stdin.readline

n = int(input())
ls = list(map(int, input().split()))
ls.sort()
group = 0
people = 0

for scared in ls:
    people += 1
    if scared == people:
        people = 0
        group += 1

print(group)
```

<br>

## 3. 곱하기 혹은 더하기
---
각 자리가 숫자 0 ~ 9로만 이루어진 문자열 S가 있을 때, 왼쪽부터 오른쪽으로 하나씩 모든 숫자를 확인하며 숫자 사이에 * 혹은 + 연산자를 넣어 결과적으로 가질 수 있는 가장 큰 수를 구하는 프로그램을 작성하시오. 단, 일반적인 우선순위와 다르게 모든 연산은 왼쪽부터 순서대로 이루어진다고 한다. 또한 만들어 질 수 있는 가장 큰 수는 항상 20억 이하의 정수가 되도록 입력이 주어진다.  
__입력 조건__  
+ 첫째 줄에 여러 개의 숫자로 구성된 하나의 문자열 S가 주어진다. (1<=S의 길이<= 20)

__출력 조건__  
+ 첫째 줄에 만들어질 수 있는 가장 큰 수를 출력한다.

```
입력 예시
02984

출력 예시
576
```

### 내가 작성한 코드
```python
# 아이디어
# 입력값이 0과 1인 경우 또는 현재 합계가 0인 경우 0이 아닌 경우는 덧셈
# 이외의 경우는 곱셈

ls = list(map(int, input()))
tot = 0
for data in ls:
    if tot == 0 or data == 0 or data == 1:
        tot += data
    else:
        tot *= data

print(tot)
```

<br>

## 4. 문자열 뒤집기
---
주인공은 0과 1로만 이루어진 문자열 S를 가지고 있다. 주인공은 이 문자열 S에 있는 모든 숫자를 전부 같게 만들려고 한다. 주인공이 할 수 있는 행동은 S에서 연속된 하나 이상의 숫자를 잡고 모두 뒤집는 것이다. 예를 들어 0001100일 때는 다음과 같다.  
1. 전체를 뒤집으면 1110011
2. 4번째 문자부터 5번째 문자까지 뒤집으면 1111111이 되어서 두 번 만에 모두 같은 숫자로 만들 수 있다.

하지만 처음부터 4번째 문자부터 5번째 문자까지 뒤집으면 모두 0으로 한 번 만에 모두 같은 숫자로 만들 수 있다. 주인공이 해야하는 행동의 최소 횟수를 구하여라.  
__입력 조건__  
+ 첫째 줄에 0과 1로만 이루어진 문자열 S가 주어진다. S의 길이는 100만보다는 작다.

__출력 조건__  
+ 첫째 줄에 주인공이 해야 하는 행동의 최소 횟수 출력

```
입력 예시
0001100

출력 예시
1
```

### 내가 작성한 코드
```python
n = list(map(int, input()))
num = n[0]
cnt = 0
key = 0

for data in n[1:]:
    # 다른 지점 도착
    # ex) 1110
    if num != data:
        key = 1

    # 다른지점에서 다시 같은 지점 도착
    # ex) 1110001
    if key == 1 and num == data:
        key = 0
        cnt += 1

# 바뀐지점에서 다시 원상태로 돌아오지 못한 경우
# ex) 111000100
if key == 1:
    cnt += 1
```
<br>

### 모범 답안
```python
data = input()
count0 = 0  # 전부 0으로 만들기 위해 뒤집기 횟수
count1 = 0  # 전부 1로 만들기 위해 뒤집기 횟수

# 두 번째 원소부터 마지막 원소 까지
for i in range(len(data) - 1):
    if data[i] != data[i + 1]:
        if data[i + 1] == '1':
            count0 += 1
        else:
            count1 += 1

# 첫 번째 원소 처리
if data[0] == '1':
    count0 += 1
else:
    count1 += 1

print(min(count1, count0))
```
i번째 원소와 i+1번째 원소가 다른 경우에서 i+1번째 원소가 1이면 1을 0으로 뒤집기 위해서 count0+=1, 반대의 경우 count1+=1을 한다. 하지만 이 경우에서는 뒤에 대상을 뒤집는 경우이므로 제일 첫 원소에 대해서는 계산을 해주지 못한다. 따라서 첫 번째 원소 처리는 따로 해준다.  
<br>

## 5. 만들 수 없는 금액
---
동네 편의점의 주인은 N개의 동전을 가지고 있다. 이때 N개의 동전을 이용하여 만들 수 없는 양의 정수 금액 중 최솟값을 구하는 프로그램을 작성하시오.  
예를 들어 N=5이고, 각 동전이 3,2,1,1,9원 짜리 동전이라고 가정하자. 이때 주인이 만들 수 없는 최소 양의 정수는 8이다.  
__입력 조건__  
+ 첫째 줄에는 동전의 개수를 나타내는 양의 정수 N이 주어진다. (1<=N<=1,000)
+ 둘째 줄에는 각 동전의 화폐 단위를 나타내는 N개의 자연수가 주어지며 공백으로 구분한다. 화폐의 단위는 1,000,000 이하의 자연수이다.

__출력 조건__  
+ 첫째 줄에 주어진 동전들로 만들 수 없는 양의 정수 금액 중 최소값을 출력

```
입력 예시
5
3 2 1 1 9

출력 예시
8
```

### 내가 생각한 풀이
```java
n = int(input())

datas = list(map(int, input().split()))
datas.sort()
target = 1

for data in datas:
    if data > target:
        break
    target += data

print(target)
```
화폐의 종류와 개수에 제한이 걸려있다. 모든 위치에서 어떤 동전을 사용했는지 기억하기는 어렵기에 dp를 사용하기에는 무리가 있다.  
점화식을 세우기 위해, 어느 지점에서 앞에 숫자까지는 다 만들 수 있었다고 가정하고 현재 숫자를 만들 수 있는지를 생각해보자.  
분명 작은 숫자부터 진행해나가니 동전은 정렬해서 하나씩 뽑아야한다.  
현재 뽑는 동전이 현재 숫자와 같거나 보다 작다면 전에 만든 합계에 더한다면 만들 수 있을 것이다.  
반면에 더 크다면 전에 만든 합계에 더해도 더 커지므로 만들 수 없게 된다.  
__항상 점화식을 세울 때는 맨 앞, 맨 끝보다는 맨 앞의 조금 뒤 혹은 맨 뒤의 조금 앞을 생각해서 가정을 세우고 고려해보는게 좋다.__

### 모범 답안
```python
n = int(input())
pays = list(map(int,input().split()))
pays.sort()
target = 1 # 이것을 만들 수 있는가?

for x in pays:
    if x>target:
        break
    target+=x

print(target)
```
이 알고리즘 설계에서는 다음과 같은 가정이 핵심이다. __1부터 target -1 까지의 모든 수를 만들 수 있다.__ 현재 target을 1로 두게 되면 0부터 0까지 금액을 만들 수 있다는 뜻이다.  
target 이전의 숫자는 무조건 만들 수 있다는 가정하에 진행하면 target 보다 작거나 같은 숫자를 뽑게되면 target은 무조건 만들 수 있게 된다. 예를 들어, 현재 target이 4이면 0부터 3까지의 금액은 만들 수 있다는 뜻이고, 여기서 2을 뽑게 된다면 0부터 3까지의 금액에 각각 2씩 더해서 총 5까지의 금액을 만들 수 있고 다음 target은 4+2인 6이 되는 것이다.  
<br>

__주어진 화폐로 해당 금액을 만들 수 있을까?__  
위의 문제를 응용해서 주어진 화폐로 주어진 금액을 만들 수 있는지 묻는 문제도 풀이할 수 있을 것 같아 혼자 코딩해보았다. 책에 있는 문제가 아니라 답안은 없지만 위의 코드를 약간만 변형해서 만들어 보았다.  
```
입력 예시
3
1 3 5
9
출력 예시
yes

입력 예시
3
1 2 4
9
출력 예시
no
```
```python
n = int(input())
pays = list(map(int,input().split()))
ans = int(input()) # 주어지는 금액
pays.sort()
target = 1

start=0 # 해당 위치부터 target-1까지 만들 수 있음
for x in pays:
    if x>target: 
        start = x 
        # target보다 x값이 크다면 x ~ x + target-1는 만들 수 있음 
    target+=x
    if target >ans : # ans보다 target이 크다면 종료
        break

if start <= ans <target:
    print('yes')
else :
    print('no')
```

<br>

## 6. 볼링공 고르기
---
A, B 두 사람이 볼링을 치고 있다. 두 사람은 무게가 서로 무게가 다른 공을 고르려고 한다. 볼링공은 총 N개 있으며 각 볼링공마다 무게가 적혀있고, 공의 번호는 1번부터 순서대로 부여된다. 또한 같은 무게의 공이 여러 개 있을 수 있지만, 서로 다른 공으로 간주한다. 볼링공의 무게는 1부터 M까지의 자연수 형태로 존재한다.  
N개의 공의 무게가 각각 주어질 때, 두 사람이 볼링공을 고르는 경우의 수를 구하는 프로그램을 작성하시오. 단, (1번공, 2번공)과 (2번공, 1번공)은 같은 경우로 간주한다.  
__입력 조건__  
+ 첫째 줄에 볼링공의 개수 N, 공의 최대 무게 M이 공백으로 구분되어 자연수 형태로 주어진다. (1<=N<=1,000, 1<=M<=10)
+ 둘째 줄에 각 볼링공의 무게 K가 공백으로 구분되어 순서대로 자연수 형태로 주어진다.(1<=K<=M)

__출력 조건__  
+ 첫째 줄에 두 사람이 볼링공을 고르는 경우의 수를 출력한다.

```
입력 예시
5 3
1 3 2 3 2

출력 예시
8
```

### 내가 작성한 코드
```python
from itertools import combinations

n,m = map(int,input().split())
weight = list(map(int,input().split()))

# 동일한 무게를 드는 경우 제거
cnt = len(list(combinations(weight, 2))) - (len(weight) - len(set(weight)))
print(cnt)
```
<br>

### 모범 답안
```python
import sys
input = sys.stdin.readline

n,m = map(int,input().split())
ball = list(map(int,input().split()))
ball_count = [0]*(m+1)
for i in ball:
    ball_count[i]+=1

result =0
for i in range(1,m+1):
    n-=ball_count[i]
    result += ball_count[i]*n
print(result)
```
A를 기준으로 생각해보면, [A가 1무게 공을 사용하는 경우의 수 * 전체 공 개수에서 1무게 공을 뺀 개수], [A가 2무게 공을 사용하는 경우의수 * 전체 공 개수에서 1무게 공 빼고 2무게공 뺀 개수] ..... 이런 방식이다. 조합이므로 A가 1무게 공을 사용하는 과정에서 1무게 사용하는 모든 경우의 수를 계산했으므로 이후의 계산에서는 1무게 공을 사용하면 안된다.

<br>

## 7. 무지의 먹방 라이브
---
[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42891){: target="_blank"}  
무지는 라이브 먹방을 하기로 했다. 회전판에 먹어야할 N개의 음식이 있다. 각 음식에는 1부터 N까지의 번호가 붙어있으며, 각 음식을 섭취하는데 일정 시간이 소요된다. 무지는 다음과 같은 방법으로 음식을 섭취한다.  
1. 무지는 1번 음식부터 먹기 시작하며, 회전판은 번호가 증가하는 순서대로 음식을 무지 앞으로 가져다 놓는다.
2. 마지막 번호의 음식을 섭취한 후에는 회전판에 의해 다시 1번 음식이 무지 앞으로 온다.
3. 무지는 음식 하나를 1초 동안 섭취한 후 남은 음식은 그대로 두고, 다음 음식을 섭취한다. 다음 음식이란, 아직 남은 음식 중 다음으로 섭취해야 할 가장 가까운 번호의 음식을 말한다.
4. 회전판이 다음 음식을 무지 앞으로 가져오는데 걸리는 시간은 없다고 가정한다.

무지가 먹방을 시작한 지 k초 후에 네트워크 장애로 잠시 중단되었다. 무지는 네트워크 정상화 후 다시 방송을 이어갈 때, 몇 번 음식부터 섭취해야하는지 알고자 한다. 각 음식을 모두 먹는 데 필요한 시간이 담겨 있는 배열 food_times, 네트워크 장애가 발생한 시간 K초가 매개변수로 주어질 때 몇 번 음식부터 다시 섭취하면 되는지 return 하도록 solution 함수를 완성하시오.  
__제한 사항__  
+ food_times는 각 음식을 모두 먹는 데 필요한 시간이 음식의 번호 순서대로 들어 있는 배열이다.
+ k는 방송이 중단된 시간을 나타낸다.
+ 만약 더 섭취해야할 음식이 없다면 -1을 반환한다.
+ food_times의 길이는 1이상 200,000이하이고, 원소는 1이상 100,000,000이하의 자연수 이다.
+ k는 1이상 2*10^13이하의 자연수이다.

```
입력 예시
3 5 # n, k
3 1 2 # food_times

출력 예시
1
```

### 내가 작성한 코드
1회차 복습시에는 풀지 못했고 답안을 확인하고 생각해서 다시 코딩했다. 답안과 비교했을 때 줄일 수 있는 코드가 좀 보인다. 나는 heappop으로 먼저 값을 빼고 while문을 돌렸는데 이럴 때는 while 루프를 나오게되면 다시 heap에 넣어줘야한다. __답안 코딩처럼 heappop을 먼저하지 말고 조건문에서 확인 후 heappop을 하면 이러한 반복을 하지 않고 효율적으로 코딩할 수 있다.__
```python
import heapq

def solution(food_times, k):
    if sum(food_times) <= k:
        return -1
    q = []

    # 우선순위 큐에 정보 담기
    for i in range(len(food_times)):
        # 소요시간, 인덱스
        heapq.heappush(q, (food_times[i], i + 1))

    # 뺄때 고민해야할점은
    # 지금까지 소요한 시간
    # 이전에 뺀것에 지금에 카운트 빼주고
    # 지금 카운트 루프 돌아도 k이하인지
    cost, idx = heapq.heappop(q)
    prev = 0  # 이전까지 먹은 누적 소요시간
    prev_count = 0  # 이전까지 먹은 음식 루프 횟수
    length = len(food_times)  # 남은 음식 개수
    # 맨위에서 걸러줬으니까 결국엔 여기서 k가 더 작아지는 경우가 생긴다.
    while prev + (cost - prev_count) * length <= k:
        prev += (cost - prev_count) * length
        prev_count = cost
        length -= 1  # 하나 빠지므로 하나씩 빼주고
        cost, idx = heapq.heappop(q)

    # while 안에서 time을 설정해버리면
    # 만약 while문을 애초에 들어가지 않는 경우 time값이 붕뜬다.
    time = k-prev
    
    # 방금 꺼낸 것에서 문제가 생겼으므로 다시 넣어주고
    heapq.heappush(q,(cost,idx))
    # while 루프에서 빠져나온 이상 남은 것을 루프 돌리기 전에 k가 맞춰진다는 뜻
    # 이제 남은 것을 한 번에 처리해야함
    # 일단 원래 음식 순서대로 풀자
    result = sorted(q, key=lambda x: x[1])

    # 1번자리에 인덱스가 들어있고,
    answer = result[(time) % length][1]

    return answer
```
<Br>

2차 리뷰 코드  
주어진 범위로 보아, 일일이 처리하는 것은 불가능하다. 한 번에 뺄 수 있는건 한 번에 처리해야 하고, 남은 것들에 대해서는 나눗셈 연산으로 처리할 생각을 했다. 매번 돌릴 때마다 food_times의 최소값을 뽑아내야 한다. 매번 최소값을 뽑아야 하는데 여기서 생각나는 것은 우선순위 큐였다.  
__답안처럼 while문 전에 heappop을 사용해서 꺼낸 뒤에 그것을 조건문의 조건으로 사용하지 않고 while 조건문에서 꺼내지않고 확인해주면서 조건문을 만족할 경우 꺼내는 형식으로 한다면 코드를 더 줄일 수 있다.__ 1차랑 똑같은 점을 느낀다.
```python
import heapq

def solution(food_times, k):
    answer=[]
    if sum(food_times)<=k:
        return -1
    q=[]
    # 정보 입력
    for i in range(len(food_times)):
        heapq.heappush(q,(food_times[i],i+1))

    # 첫 루프 뽑기
    cost, idx = heapq.heappop(q)
    prev=0 # 누적 소요시간
    prev_count=0 # 누적 루프
    length = len(food_times) # 남은 음식 개수
    # 뭉텅이로 빼는 것이 불가능 할때까지 반복
    while prev + cost * length <=k:
        prev += cost * length
        prev_count+=cost
        new_cost, idx = heapq.heappop(q)
        length-=1
        cost = new_cost-prev_count

    k -=prev # 남은 시간
    answer.append(idx)
    while q:
        cost,idx = heapq.heappop(q)
        answer.append(idx)
    answer.sort()
    return answer[k%len(answer)]
```

<Br>

3차 리뷰 코드
```python
import heapq

def solution(food_times, k):

    if sum(food_times) <= k:
        return -1

    # 계속 뽑을때 최소가 나와야함
    q=[]
    for idx in range(len(food_times)):
        # 시간과 음식번호
        heapq.heappush(q,(food_times[idx],idx+1))

    prev_tot=0 # 이전까지 먹은 총 eat
    prev_eat=0 # 이전에 먹은 eat
    length = len(food_times) # 남은 길이

    while prev_tot + (q[0][0]-prev_eat)*length <=k:
        prev_tot += (q[0][0]-prev_eat)*length
        prev_eat = heapq.heappop(q)[0]
        length-=1

    # 0부터 시작이므로 나누기만 해주면 다음에 먹을 idx가 나옴
    idx = (k-prev_tot)%length
    q.sort(key= lambda x:x[1])

    return q[idx][1]
```

### 모범 답안
일반적인 노가다로 생각하면 복잡도를 충족할 수 없다. 범위가 매우 크기때문에 어떠한 자료구조를 이용할지 생각해내야 한다.  
처음에는 테이블의 최소값으로 한 번에 빼내고 남은 값들을 일일이 확인하는 것으로 알고리즘을 설계했었다. 하지만 리스트의 길이가 너무 크고 원소의 범위도 너무 크기때문에 복잡도를 충족할 수 없었다. 풀이를 보니 여기서 조금만 더 생각해내면 됬었다. 최소값을 한 번에 빼는 것은 좋은 선택이었고 이제 남은 값들을 일일이 확인하는 과정만 줄여주면 되었던 것이다.  
이 과정을 우선순위 큐를 사용해서 정보들을 묶어서 저장하고 작은 것부터 빼내버리면 위에 생각한 과정에 배열 값이 0인 것들을 일일이 확인할 필요가 없어진다. __이 문제로부터 얻을 점은 문제에서 주어진 범위가 매우 크면 반드시 이를 처리할 자료구조를 생각해내야 한다는 점이다.__
```python
import heapq

def solution(food_times, k):
    # 전체 음식을 먹는 시간보다 k가 크거나 같다면 -1
    if sum(food_times) <= k:
        return -1

    # 시간이 작은 음식부터 빼야 하므로 우선순위 큐를 이용
    q = []
    for i in range(len(food_times)):
        # (음식 시간, 음식 번호) 형태로 우선순위 큐에 삽입
        heapq.heappush(q, (food_times[i], i + 1))  

    sum_value = 0 # 먹기 위해 사용한 시간
    previous = 0 # 직전에 다 먹은 음식 시간
    length = len(food_times) # 남은 음식의 개수

    # sum_value + (현재의 음식 시간 - 이전 음식 시간) * 현재 음식 개수와 k 비교
    while sum_value + ((q[0][0] - previous) * length) <= k:
        now = heapq.heappop(q)[0]
        sum_value += (now - previous) * length
        length -= 1 # 다 먹은 음식 제외
        previous = now # 이전 음식 시간 재설정

    # 남은 음식 중에서 몇 번째 음식인지 확인하여 출력
    result = sorted(q, key=lambda x: x[1]) # 음식의 번호 기준으로 정렬
    # +1을 해주고 나눠줘야하지 않을까? 아니다!
    # result의 인덱스는 0부터시작
    # 만약 k-sum_value의 값이 3이라면 다음 값인 4번째 값을 리턴해야함
    # 하지만 result는 인덱스 0부터 시작하므로 3이 4 번째 값임
    return result[(k - sum_value) % length][1]  
```




<br>

---
__본 포스팅은 '이것이 코딩 테스트다 with 파이썬'을 읽고 공부한 내용을 바탕으로 작성하였습니다.__
