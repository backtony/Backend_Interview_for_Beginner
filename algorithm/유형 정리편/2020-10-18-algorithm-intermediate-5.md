---
layout: post
title:  이진 탐색 기출문제
subtitle:   이진 탐색 기출문제
categories: algorithm
tags: algorithm-intermediate
comments: true
# header-img:
---
* 
{:toc}

## 1. 간단 정리
---
### 이진 탐색
탐색의 범위를 반으로 줄여나가면서 데이터를 빠르게 탐색하는 탐색 기법이다. 이진 탐색은 배열 __내부의 데이터가 정렬되어 있을 때만__ 사용할 수 있으며, 이진 탐색 알고리즘에서는 3가지 변수를 사용한다(시작점, 끝점, 중간점)  
시작점, 끝점은 탐색하고자 하는 범위를 나타내기 위해 사용하며, 탐색 범위의 중간점에 있는 데이터와 찾고자 하는 데이터를 비교한다.  
__이진탐색을 사용해야 하는 문제의 특징은 엄청나게 넓은 범위에서 특정한 지점을 찾아야 하는 것이다.__

### bisect 클래스
__단순히 정렬된 배열에서 특정한 데이터를 찾도록 요구하는 문제__ 에서는 이진 탐색을 직접 구현할 필요 없이 단순히 파이썬의 표준 라이브러리 중에서 bisect 모듈을 사용하여 right, left의 인자로 같은 값을 주게되면 위치를 찾을 수 있다. bisect와 bisect_right은 같은 동작을 한다.
```python
from bisect import bisect_left,bisect_right

a = [1,2,4,4,8]
print(bisect_left(a,4)) # 2 # 4가 들어가야할 가장 왼쪽 인덱스 반환
print(bisect_right(a,4)) # 4 # 4가 들어가야할 가장 오른쪽 인덱스 반환
# left는 값의 제일 왼쪽 수의 인덱스를 반환하지만
# right는 값의 제일 오른쪽 수의 +1 인덱스 값을 반환한다.

# 만약 문자열에서 사용할 경우 문자열개수우선이 아니라 각 자리에 맞춰서 우선순위에 따라 값을 반환한다
['frame', 'frodo', 'front', 'frost', 'frozen', 'kakao']
print(bisect_right(a,'frozz')) # 5가 반환된다. 4가 아니다!! 주의해라.
```
<br>

## 2. 정렬된 배열에서 특정 수의 개수 구하기
---
N개의 원소를 포함하고 있는 수열이 오름차순으로 정렬되어 있다. 이때 수열에서 x가 등장하는 횟수를 계산하시오. 시간복잡도는 O(logN)으로 설계해야한다.  
__입력 조건__  
+ 첫째 줄에 N과 x가 정수 형태로 공백으로 구분되어 입력된다. (1<=N<=1,000,000), (-10^9<=x<=10^9)
+ 둘째 줄에 N개의 원소가 정수 형태로 공백으로 구분되어 입력된다 (-10^9<=각 원소의 값<=10^9)

__출력 조건__  
+ 수열의 원소 중에서 값이 x인 원소의 개수를 출력한다. 단 x인 값이 없다면 -1을 출력한다.

```
입력 예시
7 2
1 1 2 2 2 2 3

출력 예시
4

입력 예시
7 4
1 1 2 2 2 2 3

출력 예시
-1
```

### 내가 작성한 코드
```python
from bisect import bisect_left, bisect_right

n, x = map(int, input().split())
table = list(map(int, input().split()))

start = bisect_left(table, x)
end = bisect_right(table, x)
ans = end - start
if ans == 0:
    print(-1)
else:
    print(ans)
```

### 모범 답안
```python
from bisect import bisect_left, bisect_right

# 값이 [left_value, right_value]인 데이터의 개수를 반환하는 함수
def count_by_range(array, left_value, right_value):
    right_index = bisect_right(array, right_value)
    left_index = bisect_left(array, left_value)
    return right_index - left_index

n, x = map(int, input().split()) # 데이터의 개수 N, 찾고자 하는 값 x 입력 받기
array = list(map(int, input().split())) # 전체 데이터 입력 받기

# 값이 [x, x] 범위에 있는 데이터의 개수 계산
count = count_by_range(array, x, x)

# 값이 x인 원소가 존재하지 않는다면
if count == 0:
    print(-1)
# 값이 x인 원소가 존재한다면
else:
    print(count)
```
내 코드와 다른 부분은 단지 함수를 따로 만들어서 사용했다는 점
<br>

## 3. 고정점 찾기
---
고정점이란, 수열의 원소 중에서 그 값이 인덱스와 동일한 원소를 의미한다. 하나의 수열이 N개의 서로 다른 원소를 포함하고 있으며, 모든 원소가 오름차순으로 정렬되어 있다. 이때 이 수열에서 단 하나의 고정점이 있다고 가정하고, 고정점을 출력하는 프로그램을 작성하시오. 없다면 -1을 출력하시오. 시간 복잡도는 O(logN)으로 설계해야 한다.  
__입력 조건__  
+ 첫째 줄에 N이 입력 된다.(1<= N <= 1,000,000)
+ 둘째 줄에 N개의 원소가 정수 형태로 공백으로 구분되어 입력된다. (-10^9<= 각 원소의 값 <=10^9)

__출력 조건__  
+ 고정점을 출력하고 없다면 -1을 출력한다.

```
입력 예시
5
-15 -6 1 3 7 

출력 예시
3

입력 예시
7
-15 -4 2 8 9 13 15

출력 예시
2

입력 예시
7
-15 -4 3 8 9 13 15

출력 예시
-1
```

### 내가 작성한 코드
```python
def binary_search(start, end):
    # 순서가 역전되면 찾지 못함을 의미
    if start > end:
        return -1
    mid = (start + end) // 2
    # 찾으면 인덱스 반환
    if table[mid] == mid:
        return mid
    # 찾지 못했을 경우 start,end 수정
    if table[mid] > mid:
        end = mid - 1
    else:
        start = mid + 1
    # 수정한 값을 가지고 다시 이진탐색
    return binary_search(start, end)


n = int(input())
table = list(map(int, input().split()))
print(binary_search(0, n - 1))
```

### 모범 답안
```python
def binary_search(a,start,end):
    mid = (start+end)//2
    if start>end:
        return -1
    elif a[mid]==mid:
        return mid
    elif a[mid]>mid:
        return binary_search(a,start,mid-1)
    elif a[mid]<mid:
        return binary_search(a,mid+1,end)

# 문제 조건에 따라 이진 탐색을 사용해야 한다.
# 수열은 오름차순으로 정렬되어있으므로 바로 이진 탐색을 사용할 수 있다

n = int(input())
num = list(map(int,input().split()))
ans = binary_search(num,0,n-1)
print(ans)
```
문제 조건에 따라 이진 탐색을 사용해야 하고, 수열은 오름차순으로 이미 정렬되어 있으므로 바로 이진 탐색을 사용할 수 있다. 고정점은 인덱스 값과 해당 값이 같은 점이므로 이진 탐색으로 쉽게 풀 수 있다.
<br>

## 4. 공유기 설치
---
[문제 클릭](https://www.acmicpc.net/problem/2110){: target="_blank"}  

### 내가 작성한 코드
```python
n, c = map(int, input().split())
home = []

for _ in range(n):
    home.append(int(input()))

home.sort()
start = 1
end = home[-1] - home[0]
ans = 0
while start <= end:
    mid = (start + end) // 2
    cnt = 1
    target = home[0] + mid
    for next in home[1:]:
        if target <= next:
            target = next + mid
            cnt += 1

    if cnt >= c:
        start = mid + 1
        ans = max(ans, mid)

    else:
        end = mid - 1


print(ans)
```
1. 범위가 매우 크고 특정 값을 찾는 것이므로 이진 탐색이다.
2. 이진 탐색은 정렬되어야 적용할 수 있으므로 정렬한다.
3. 이진 탐색을 진행하기 위해서는 거리의 기준이 되는 __start와 end 지점을 찾아야 한다.__
4. 가장 끝점과 첫 지점의 차이가 end일 것이고 가장 짧은 거리는 1이 된다.
5. start와 end를 이용해 mid를 구하고, 어떤 경우 start=mid+1, 어떤 경우 end = mid-1 로 할지 __기준을 정한다.__
6. 첫 집을 시작점으로 하여 mid만큼 뛰어서 공유기 설치 개수에 따른 기준을 만들고 start와 end를 조정한다.
7. start와 end가 역전되면 종료한다.

### 모범 답안
가장 인접한 두 공유기 사이의 거리의 최댓값을 탐색해야 하는 문제로 이해할 수 있다. 이때 각 집의 좌표가 최대 10억이므로, 이진 탐색을 이용하여 문제를 해결해야 한다. 따라서 이진 탐색으로 가장 인접한 두 공유기 사이의 거리를 조절해가며, 매 순간 실제로 공유기를 설치하여 C보다 많은 개수로 공유기를 설치할 수 있는지 체크하여 문제를 해결할 수 있다. 다만 가장 인접한 두 공유기 사이의 거리의 최댓값을 찾아야 하므로, C보다 많은 개수로 공유기를 설치할 수 있다면 가장 인접한 두 공유기 사이의 거리를 증가시켜 더 큰 값에 대해서도 성립하는지 체크하기 위해 다시 탐색을 수행한다.
```python
# 집의 개수(N)와 공유기의 개수(C)를 입력 받기
n, c = list(map(int, input().split(' ')))

# 전체 집의 좌표 정보를 입력 받기
array = []
for _ in range(n):
     array.append(int(input()))
array.sort() # 이진 탐색 수행을 위해 정렬 수행

start = 1 # 가능한 최소 거리(min gap)
end = array[-1] - array[0] # 가능한 최대 거리(max gap)
result = 0

while(start <= end):
    mid = (start + end) // 2 # mid는 가장 인접한 두 공유기 사이의 거리(gap)을 의미
    # 첫째 집에는 무조건 공유기를 설치한다고 가정
    value = array[0]
    count = 1
    # 현재의 mid 값을 이용해 공유기를 설치하기
    for i in range(1, n): # 앞에서부터 차근차근 설치 
        if array[i] >= value + mid:
            value = array[i]
            count += 1
    if count >= c: # C개 이상의 공유기를 설치할 수 있는 경우, 거리를 증가시키기
        start = mid + 1
        result = mid # 최적의 결과를 저장
    else: # C개 이상의 공유기를 설치할 수 없는 경우, 거리를 감소시키기
        end = mid - 1

print(result)
```

__내가 왜 답안처럼 접근을 못 했을까?__  
이진 탐색에 대해 다시 생각해보자. 이진 탐색은 탐색의 방법 중에 탐색을 빠르게 해주는 방법이다. 탐색이란 무엇인가? 컴퓨터에서 탐색 자체는 원래 원초적인 것이다. 예를 들자면, 조건에 맞는 숫자를 찾도록 0부터 시작해서 주어진 범위까지 차례대로 비교해가면서 확인하는 것이다. 근데 원초적인 방법으로 탐색을 하면 시간이 너무 오래걸리기 때문에 이진 탐색을 사용하는 것이다. 이진 탐색은 원초적인 방법과 다르게 시작을 0부터 하는 것이 아니라 주어진 범위 내에서 중간값을 찾는 값이라고 가정하고 비교해가면서 진행하는 과정이다.  
그렇다면 위의 문제에는 어떻게 적용되었나 생각해보자. 가장 인접한 공유기 사이의 최대거리를 찾아야한다. 즉, 탐색해야 한다는 것이다. 위에서 말했다싶이 탐색은 원초적이다. 최대 거리를 1이라고 가정하고 범위내에서 값을 증가시켜가면서 조건이 맞는 최대 거리를 찾으면 되는 것이다. 그렇다면 이 과정을 빠르게 수행하기 위해서 이진탐색을 사용하는 것이 이 문제의 핵심이다. 최대거리를 1부터 시작하는게 아니라 주어진 범위 내에서 중간점을 최대거리라고 가정하고 이진탐색으로 찾아나가는 것이다.
<br>

## 5. 가사 검색
---
[문제 클릭](https://programmers.co.kr/learn/courses/30/lessons/60060){: target="_blank"}  

### 내가 작성한 코드
단어를 알파벳 하나씩 모두 비교하게 되면 단어 하나의 최대 길이가 1억이기 때문에 시간 초과가 발생한다.  
비교, 아주 큰 범위 -> 이진 탐색을 생각해야 한다.  
파이썬의 sort 기능은 글자수에 관계없이 우선순위에 따라 정렬되기 때문에 1차적으로 글자수에 따른 분류를 진행하고 이진 탐색을 진행해야 한다.  
파이썬에서 역순 출력은 [::-1]을 이용하면 된다.  
[a:b:c] 문법은 배열의 인덱스 a부터 b까지 인덱스 간격 c으로 배열을 생성한다.

```python
from bisect import bisect_left,bisect_right

def solution(words, queries):


    result=[]
    reverseWords=[[] for _ in range(10001)]
    originWords=[[] for _ in range(10001)]

    for word in words:
        length = len(word)
        reverseWords[length].append(word[::-1])
        originWords[length].append(word)

    for i in range(1,10001):
        reverseWords[i].sort()
        originWords[i].sort()

    for query in queries:
        length = len(query)

        start = query.replace('?', 'a')
        end = query.replace('?', 'z')

        if query[-1] == '?':
            cnt = bisect_right(originWords[length],end) - bisect_left(originWords[length],start)
        else:
            cnt = bisect_right(reverseWords[length], end[::-1]) - bisect_left(reverseWords[length], start[::-1])

        result.append(cnt)

    return result
```


### 모범 답안
bisect는 각 자리끼리의 우선순위를 판단해서 인덱스 값을 반환한다. 예를 들어 a=[frodo, frozen]와 같이 정렬된 리스트가 있을 때 bisect_right(a,'frozz')를 사용하면 1이 아니라 2를 반환한다. 즉, 문자열의 길이를 고려하지 않고 사전순으로 찾아간다는 뜻이다. 따라서 이 문제와 같이 __넓은 범위 내에서 특정위치를 찾아가야하는데 문자열의 길이를 고려해야 한다면 bisect를 사용하기 전에 우선 문자열의 길이를 기준으로 리스트를 따로 선언한 후 사용해야 한다는 점을 반드시 기억하자.__  
'?'이 뒤쪽에 있는 경우는 '?'을 'a'와 'z'로 교체하고 비교하면 쉽게 구할 수 있다. 하지만 '?'가 맨 앞에 있는 경우는 다른 방법을 생각해내야 한다. 왜냐하면 앞에 있는 '?'를 'a'와 'z'로 바꾸게 되면 당연히 맨 앞과 맨 뒤를 차지하게되어 모든 단어를 포함하게 되기 때문이다. 그렇다면 '?'를 뒤로 옮기기위해서 뒤집으면 어떨까? 괜찮다. 왜냐하면 구하는 것은 각 인덱스에 해당하는 문자가 같은지 판단하는 것이기 때문이다.
자주 사용되진 않지만 풀이에 사용된 replace 함수의 사용법도 기억해두고, 리스트를 [::-1]로 뒤집는 방법도 기억해두자.  
```python
from bisect import bisect_left, bisect_right

# 값이 [left_value, right_value]인 데이터의 개수를 반환하는 함수
def count_by_range(a, left_value, right_value):
    right_index = bisect_right(a, right_value)
    left_index = bisect_left(a, left_value)
    return right_index - left_index

# 모든 단어들을 길이마다 나누어서 저장하기 위한 리스트
array = [[] for _ in range(10001)]
# 모든 단어들을 길이마다 나누어서 뒤집어 저장하기 위한 리스트
reversed_array = [[] for _ in range(10001)]

def solution(words, queries):
    answer = []
    for word in words: # 모든 단어를 접미사 와일드카드 배열, 접두사 와일드카드 배열에 각각 삽입
        array[len(word)].append(word) # 단어를 삽입
        reversed_array[len(word)].append(word[::-1]) # 단어를 뒤집어서 삽입

    for i in range(10001): # 이진 탐색을 수행하기 위해 각 단어 리스트 정렬 수행
        array[i].sort()
        reversed_array[i].sort()

    for q in queries: # 쿼리를 하나씩 확인하며 처리
        if q[0] != '?': # 접미사에 와일드 카드가 붙은 경우
            res = count_by_range(array[len(q)], q.replace('?', 'a'), q.replace('?', 'z'))
        else: # 접두사에 와일드 카드가 붙은 경우
            res = count_by_range(reversed_array[len(q)], q[::-1].replace('?', 'a'), q[::-1].replace('?', 'z'))
        # 검색된 단어의 개수를 저장
        answer.append(res)
    return answer
```

__이 문제에서 배울점__  
사실 문자열 비교는 일일이 비교하거나, c언어의 strcmp밖에 생각나지 않았다. __파이썬에서는 위 문제와 같이 앞이나 뒤에 문자열이 같은지를 확인하는 경우 문자열 길이별로 저장, 정렬한 뒤에 문자를 수정하거나 추가해 이진탐색을 이용하여 일치하는 문자열을 찾을 수 있다는 점을 반드시 기억해두자. 하지만 앞,뒤가 아닌 중간에서 일치하는 여부는 다른 방법을 생각해야한다.__


<br>


## 이진탐색 느낀점
범위가 매우 큰 상태에서 어떤 것을 찾는다면 이진탐색을 가장 먼저 떠올려야 한다.  
이진탐색은 __거리를 기준__ 으로 특정 지점을 찾기 때문에 풀이방식이 이진탐색이라는 것을 떠올렸다면 가장 먼저 기준으로 잡을 거리 __start,end를 찾아야 한다.__  
쉬운 문제라면 간단하게 start,end 만으로 특정 지점을 찾아서 정답을 도출한다.  
__어려운 문제라면 이진탐색으로 찾아낸 mid를 이용해 추가적인 로직으로 해당 mid가 정답이 맞는지 판단하고 아니라면 다시 이진탐색으로 mid를 찾아 판단하는 구조로 풀이가 진행된다.__


<br>


---
__본 포스팅은 '이것이 코딩 테스트다 with 파이썬'을 읽고 공부한 내용을 바탕으로 작성하였습니다.__
