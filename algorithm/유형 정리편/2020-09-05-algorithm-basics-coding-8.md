---
layout: post
title:  이진 탐색 with 파이썬
subtitle:   이진 탐색 with 파이썬
categories: algorithm
tags: algorithm-basics
comments: true
# header-img:
---
* 
{:toc}


## 1. 순차 탐색
---
순차 탐색이란 리스트 안에 있는 특정한 데이터를 찾기 위해 앞에서부터 데이터를 하나씩 차례대로 확인하는 방법이다. 리스트 자료형에서 특정한 값을 가지는 원소의 개수를 세는 count() 메서드를 이용할 때도 내부에서는 순차 탐색이 수행된다.  
```python
def sequential_search(n,target,arry):
    for i in range(n):
        if arry[i]==target:
            return i+1

input_data = input().split() # 원소의 개수와 한칸 띄고 찾을 문자열 입력
n = int(input_data[0]) # 원소의 개수
target = input_data[1] # 찾고자 하는 문자열

arry = input().split() # 적은 원소 개수만큼 문자열 입력

print(f"{sequential_search(n,target,arry)} 번째 문자열")
```
<br>

## 2. 이진 탐색
---
이진 탐색은 __배열 내부의 데이터가 정렬되어 있어야만 사용__ 할 수 있는 알고리즘이다. 데이터가 무작위일 때는 사용할 수 없지만, 이미 정렬되어 있다면 매우 빠르게 데이터를 찾을 수 있다는 특징이 있다. 이진 탐색은 위치를 나타내는 변수를 3개 사용하는데 탐색하고자 하는 범위의 시작점, 끝점, 중간점이다. 찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교해서 원하는 데이터를 찾는 게 이진 탐색 과정이다.  
확인 과정에서 원소가 절반씩 줄어든다는 점에서 시간 복잡도는 O(logN)이다.  
__재귀 함수로 구현__  
```python
def binary_search(arry,target,start,end):
    if start> end:
        return None
    mid = (start+end)//2
    if arry[mid]==target:
        return mid
    elif arry[mid]<target:
        start=mid+1
        return binary_search(arry,target,start,end)
    else :
        end=mid-1
        return binary_search(arry,target,start,end)

arry = list(map(int,input().split()))
target = int(input())
n=len(arry)
idx = binary_search(arry,target,0,n-1)
if idx == None:
    print("없다")
else :
    print(f"{idx+1}번 째 숫자이다.")
```

__반복문으로 구현__  
재귀를 반복문으로 구현하려면 while문이면 충분하다.
```python
def binary_search(arry,target,start,end):
    while start<=end:        
        mid = (start+end)//2
        if arry[mid]==target:
            return mid
        elif arry[mid]<target:
            start=mid+1            
        else :
            end=mid-1
    return None
            

arry = list(map(int,input().split()))
target = int(input())
n=len(arry)
idx = binary_search(arry,target,0,n-1)
if idx == None:
    print("없다")
else :
    print(f"{idx+1}번 째 숫자이다.")
```
<br>

__cf) 코딩 테스트에서의 이진 탐색__  
이진 탐색은 코딩 테스트에서 단골로 나오는 문제이니 가급적 외워두는 것이 좋다. 이진 탐색 문제는 탐색 범위가 큰 상황에서의 탐색을 가정하는 문제가 많다. 따라서 탐색 범위가 2,000만을 넘어가면 이진 탐색으로 문제에 접근을 고려해봐야 한다. 처리해야 할 데이터의 개수나 값이 1,000만 단위 이상으로 넘어가면 이진 탐색과 같이 O(logN)의 속도를 내야하는 알고리즘을 떠올려야 문제를 풀 수 있는 경우가 많으니 기억하자.  

## 3. 이진 탐색 트리
---
큰 데이터를 처리하는 소프트웨어는 대부분 데이터를 트리 자료구조로 저장해서 이진 탐색과 같은 탐색 기법을 이용해 빠르게 탐색이 가능하다.  
__이진 탐색 트리의 특징__  
+ 부모 노드보다 왼쪽 자식 노드가 작다.
+ 부모 노드보다 오른쪽 자식 노드가 크다.

이진 탐색 문제는 입력 데이터가 많거나 탐색 범위가 매우 넓은 편이다. 따라서 input을 쓰기보다는 sys 라이브러리의 readline() 함수를 사용하자.  
<br>

## 4. 실전 문제
---
### 문제 : 부품 찾기
전자 매장에는 부품이 N개가 있고 각 부품은 정수 형태의 고유번호가 있다. 손님이 M개의 종류의 부품을 대량으로 구매하겠다고 견적서를 보냈고 직원은 문의한 부품 M개의 종류를 모두 확인해서 견적서를 작성해야 한다. 이때 손님이 요청한 부품 번호의 순서대로 부품을 확인해서 부품이 있으면 yes 없으면 no를 출력한다. 구분은 공백으로 한다.  
__입력 조건__  
+ 첫째 줄에는 정수 N이 주어진다. (1<=N<=1,000,000)
+ 둘째 줄에는 공백으로 구분하여 N개의 정수가 주어진다. 정수는 1 ~ 1,000,000 사이
+ 셋째 줄에는 정수 M이 주어진다. N과 범위 동일
+ 넷째 줄에는 공백으로 구분하여 M개의 정수가 주어진다. 정수는 1보다 크고 10억 이하이다.

__출력 조건__  
+ 첫째 줄에 공백으로 구분하여 각 부품이 존해자면 yes 아니면 no 출력

```
입력 예시
5
8 3 7 9 2
3 
5 7 9

출력 예시
no yes yes
```

#### 풀이 : 이진 탐색
주어진 M의 개수가 최대 100만이고 N과 비교하는 과정이 필요하므로 연산횟수가 1,000만 단위를 넘어간다. 따라서 count 메서드는 순차탐색 O(N)의 시간 복잡도를 가지므로 사용할 수 없다. 이진 탐색의 복잡도는 O(logN)이므로 이진 탐색을 사용하도록 하자. 이진 탐색을 위해서는 먼저 정렬되어있어야 한다는 점을 기억하자.  
```python
import sys

def binary_search(ls, target, start, end):
    while start <= end:
        mid = (start + end) // 2
        if target == ls[mid]:
            return True
        elif target < ls[mid]:
            end = mid - 1
        else:
            start = mid + 1
    return False

input = sys.stdin.readline

n = int(input())
budget = list(map(int, input().split()))
budget.sort()

m = int(input())
request = list(map(int, input().split()))


for i in request:
    if binary_search(budget, i, 0, n - 1):
        print("yes",end=" ")
    else:
        print("no",end =" ")
```
이진 탐색을 M번 반복하므로 O(M * logN)의 연산이 필요하다. 이론상 최대 약 200만 번의 연산이 이루어진다고 할 수 있다. N개의 부품을 정렬하기 위해서는 O(NlogN)이므로 전체적인 시간 복잡도는 O((N+M) * logN)이다.  
<br>

#### 풀이 : set함수
단순히 특정한 수가 한 번이라도 등장했는지를 검사하면 되므로 set()함수를 이용할 수 있다. set()함수는 파이썬에서 집합을 표현할 때 사용하는 자료형이다. 따라서 단순히 특정한 데이터가 존재하는지 검사할 때에 매우 효과적이고 간결한 측면에서는 가장 우수하다.  
```python
import sys

input = sys.stdin.readline

n = int(input())
budget = set(map(int, input().split()))

m = int(input())
request = list(map(int, input().split()))

for i in request:
    if i in budget:
        print("yes",end=" ")
    else:
        print("no",end =" ")
```

__cf) in 의 시간 복잡도__  
__list, tuple__  
Average: O(n)  
하나하나 순회하기 때문에 데이터의 크기만큼 시간 복잡도를 갖게 된다.  

__set, dictionary__  
Average: O(1), Worst: O(n)
__내부적으로 hash를 통해서 자료들을 저장__ 하기 때문에 시간복잡도가 O(1)가 가능하고 O(n)의 경우에는 해시가 성능이 떨어졌을(충돌이 많은 경우) 때 발생한다.  

<br>

#### 풀이 : 계수 정렬
입력되는 부품의 개수가 많다면 효율적이지만 적다면 공간 복잡도가 매우 비효율적일 수도 있다.
```python
import sys

shop_list = [0]*1000001

N = int(sys.stdin.readline().rstrip())
for i in sys.stdin.readline().rstrip().split():
    shop_list[int(i)]=1

M = int(sys.stdin.readline().rstrip())
for i in sys.stdin.readline().rstrip().split():
    if shop_list[int(i)]==1:
        print("yes",end=" ")
    else :
        print("no",end=" ")
```

<br>   

### 문제 : 떡볶이 떡 만들기
절단기에 높이를 지정하면 줄지어진 떡을 한 번에 절단한다. 높이가 H보다 긴 떡은 H위의 부분이 잘릴 것이고, 낮은 떡은 잘리지 않는다. 예를 들어 19 14 10 17 cm인 떡이 있고 절단기 높이가 15라면 4 0 0 2 만큼이 절단될 것이다. 그렇다면 손님은 총 6cm만큼의 길이를 가져가게 된다.  
손님이 요청한 길이가 M일 때 적어도 M만큼의 떡을 얻기 위해 절단기에 설정할 수 있는 높이의 최댓값을 구하는 프로그램을 작성하시오.  
__입력 조건__  
+ 첫째 줄에 떡의 개수 N과 요청한 떡의 길이 M이 주어진다.(1<=N=1,000,000 , 1<=M<=2,000,000,000)
+ 둘째 줄에는 떡의 개별 높이가 주어진다. 떡 높이의 총 합은 항상 M이상이므로, 손님은 필요한 양만큼 떡을 사갈 수 있다.

__출력 조건__  
+ 적어도 M만큼의 떡을 집에 가져가기 위해 절단기에 설정할 수 있는 높이의 최댓값을 출력한다.

```
입력 예시
4 6
19 15 10 17

출력 예시
15
```

#### 풀이
__잘못된 풀이__  
```python
import sys

N,M = map(int,sys.stdin.readline().rstrip().split())
arry = list(map(int,sys.stdin.readline().rstrip().split()))

max_length = max(arry)
for delete in range(1,max_length+1):
    count =0
    for i in range(len(arry)):
        if arry[i]-(max_length-delete)>0:
            count+=arry[i]-(max_length-delete)
    if count>=M:
        break
print(max_length-delete)
```
처음 시도에서는 이렇게 풀었다. 하지만 위와 같이 풀면 반드시 시간 초과가 나올 수밖에 없다. __M의 범위가 10억까지이므로 이렇게 큰 수의 경우 반드시 이진 탐색을 먼저 떠올려야 한다.__    
<br>

__올바른 풀이__  
이진 탐색을 떠올려야하는 이유는 위에서 설명했다. 이 문제는 전형적인 이진 탐색 문제이자, 파라메트릭 서치 유형의 문제이다. 파라메트릭 서치는 최적화 문제를 결정 문제(예 아니오로 답하는 문제)로 바꾸어 해결하는 기법이다. 원하는 조건을 만족하는 가장 알맞은 값을 찾는 문제에서 주로 파라메트릭 서치를 이용한다. 예를 들어 범위 내에서 조건을 만족하는 가장 큰 값을 찾으라는 최적화 문제라면 이진 탐색으로 결정 문제를 해결하면서 범위를 좁혀갈 수 있다. 코딩 테스트나 프로그래밍 대회에서는 보통 파라메트릭 서치 유형은 이진 탐색으로 해결한다.  
```python
n, m = map(int, input().split())
dduck = list(map(int, input().split()))


def binary(graph, target, start, end):
    while start <= end:
        ans = 0
        mid = (start + end) // 2
        for i in dduck:
            if i - mid > 0:
                ans += i - mid
        if ans == target:
            return mid
        if ans < target:
            end = mid - 1
        else:
            start = mid + 1
    # 항상 ans는 타켓 이상이어야 함.
    return end


print(binary(dduck, m, 0, max(dduck)))
```


---
__본 포스팅은 '이것이 코딩 테스트다 with 파이썬'을 읽고 공부한 내용을 바탕으로 작성하였습니다.__


