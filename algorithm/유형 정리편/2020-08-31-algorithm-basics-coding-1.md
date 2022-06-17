---
layout: post
title:  주요 라이브러리의 문법과 유의점
subtitle:   주요 라이브러리의 문법과 유의점
categories: algorithm
tags: algorithm-basics
comments: true
# header-img:
---
* 
{:toc}

## 개요
---
본격적으로 알고리즘을 공부하기 앞서 파이썬의 기초이론과 라이브러리의 문법을 복기하기 위해서 작성한다.  
<br>

## 1. 입출력: sys
---
지금까지 기초에서 입력을 받을때는 input()을 사용해왔다. 하지만 알고리즘 풀이에서 입력을 최대한 빠르게 받아야 하는 경우가 있다. 흔히 정렬, 이진 탐색, 최단 경로 문제의 경우 매우 많은 수의 데이터가 연속적으로 입력이 되곤 한다. 예를 들어 1,000만 개가 넘는 라인이 입력되는 경우, 입력을 받는 것만으로도 시간 초과를 받을 수 있다. 따라서 파이썬의 경우 입력의 개수가 많은 경우에는 단순히 input() 함수를 그대로 사용하지는 않는다. input() 함수는 동작 속도가 느려서 시간 초과로 오답 판정을 받을 수 있기 때문이다. 이 경우 파이썬의 sys 라이브러리에 정의되어 있는 sys.stdin.readline() 함수를 사용한다. readline()으로 입력시 입력 후 엔터가 줄 바꿈 기호로 입력되는데, 이 공백 문자를 제거하기 위해 rstrip()함수를 사용해야 한다. 
```
# 사용법
import sys
sys.stdin.readline().rstrip()

a,b = map(int,sys.stdin.readline().rstrip().split())
print(a,b)
```
<br>

## 2. 주요 라이브러리의 문법과 유의점
---
표준 라이브러리란 특정한 프로그래밍 언어에서 자주 사용되는 표준 소스코드를 미리 구현해 놓은 라이브러리를 의미한다. 코딩 테스트를 준비하며 반드시 알아야 하는 파이썬의 라이브러리는 6가지 정도이다.  
+ 내장 함수 : print(), input()과 같은 기본 입출력 기능부터 sorted()와 같은 정렬 기능을 포함하고 있는 기본 내장 라이브러리이다.
+ itertools : 파이썬에서 반복되는 형태의 데이터를 처리하는 기능을 제공하는 라이브러리이다. 순열과 조합 라이브러리를 제공한다.
+ heapq : 힙 기능을 제공하는 라이브러리이다.
+ bisect : 이진 탐색 기능을 제공하는 라이브러리이다.
+ collections : 덱, 카운터 등의 유용한 자료구조를 포함하고 있는 라이브러리이다.
+ math : 필수적인 수학 기능을 제공하는 라이브러리이다. 팩토리얼, 제곱근, 최대공약수, 삼각함수 관련 함수부터 파이와 같은 상수를 포함한다.

### 내장함수
파이썬에서는 별도의 import 명령어 없이 바로 사용할 수 있는 내장 함수가 존재한다. 

#### sum
sum() 함수는 리스트와 같은 iterable 객체가 입력으로 주어졌을 때, 모든 원소의 합을 반환한다.
```python
result = sum([1,2,3,4,5]) # 15
```

#### min, max
min() 함수는 파라미터가 2개 이상 들어왔을 때 작은 값을, max는 가장 큰 값을 반환한다.
```python
result = min(7,3,5,2) # 2
result = max(7,3,5,2) # 7
```

#### eval
eval() 함수는 수학 수식이 문자열 형식으로 들어오면 해당 수식을 계산한 결과를 반환한다.
```python
result = eval("(3+5)*7") # 56
```

#### sorted
sorted() 함수는 iterable 객체가 들어왔을 때, 정렬된 결과를 반환한다. reverse 속성으로 결과를 뒤집을 수도 있다.
```python
result = sorted([9,1,8,5,4]) # [1,4,5,8,9]
result = sorted([9,1,8,5,4],reverse = True) # [9,8,5,4,1]
```
<br>

파이썬에서는 리스트의 원소로 리스트나 튜플이 존재할 때 특정한 기준에 따라서 정렬을 수행할 수 있다. 정렬 기준은 key 속성을 이용해 명시할 수 있다. key 인자에 함수를 넘겨주면 해당 함수의 반환값을 비교하여 순서대로 정렬한다.  
예를 들어 리스트 [('홍길동',35), ('이순신',75),('아무개',50)]이 있을 때, 원소를 튜플의 두 번째 원소를 기준으로 내림차순으로 정렬하고자 한다면 다음과 같다.
```python
result = sorted([('홍길동',35), ('이순신',75),('아무개',50)],key = lambda x: x[1],reverse = True)
```
<br>

첫 번째 인자를 기준으로 오름차순으로 먼저 정렬하고, 안에서 다음 두 번째 인자를 기준으로 내림차순으로 정렬하게 하려면, 다음과 같이 할 수 있다.  
```python
e = [(1, 3), (0, 3), (1, 4), (1, 5), (0, 1), (2, 4)] 
f = sorted(e, key = lambda x : (x[0], -x[1])) 
# f = [(0, 3), (0, 1), (1, 5), (1, 4), (1, 3), (2, 4)]
# sorted 기본이 오름차순이므로 -를 붙이면 자연스레 내림차순이 된다.
```

#### sort
리스트와 같은 iterable 객체는 기본적으로 sort() 함수가 내장하고 있어 굳이 sorted() 함수를 사용하지 않아도 된다.  
```
data = [9,1,8,5,4]
data.sort() # [1,4,5,8,9]
```

### itertools
itertools는 파이썬에서 반복되는 데이터를 처리하는 기능을 포함하는 라이브러리이다. 제공하는 클래스는 매우 다양하지만, 코딩 테스트에서 가장 유용하게 사용할 수 있는 클래스는 permutations, combinations이다.  

#### 순열
permutations는 리스트와 같은 iterable 객체에서 r개의 데이터를 뽑아 일렬로 나열하는 모든 경우(순열)을 계산해준다. permutations는 클래스이므로 객체 초기화 이후에는 __리스트 자료형__ 으로 변환하여 사용한다. 리스트 ['A' , 'B' , 'C']에서 3개를 뽑아 나열하는 모든 경우를 출력하면 다음과 같다.  
__만약 두번째 인자를 생략한다면, 첫 번째 인자의 길이로 들어간다.__
```python
from itertools import permutations
data = ['A','B','C']
result = list(permutations(data,3))
print(result)
# [('A', 'B', 'C'), ('A', 'C', 'B'), ('B', 'A', 'C'), ('B', 'C', 'A'), ('C', 'A', 'B'), ('C', 'B', 'A')]

# 만약 2번째 인자를 생략할 경우, 첫 인자의 길이가 default로 들어간다.
result = list(permutations(data))
print(result)
# [('A', 'B', 'C'), ('A', 'C', 'B'), ('B', 'A', 'C'), ('B', 'C', 'A'), ('C', 'A', 'B'), ('C', 'B', 'A')]
```
<br>

#### 조합
combinations는 리스트와 같은 iterable 객체에서 r개의 데이터를 뽑아 순서를 고려하지 않고 나열하는 모든 경우(조합)을 계산한다. combinations는 클래스이므로 객체 초기화 이후에는 __리스트 자료형__ 으로 변환하여 사용한다. 리스트 ['A' , 'B' , 'C']에서 2개를 뽑아 순서에 상관없이 나열하는 모든 경우를 출력하면 다음과 같다.  
permutations과 달리 두번째 인자를 생략할 수 없다.
```python
from itertools import combinations
data = ['A','B','C']
result = list(combinations(data,2))
print(result)
# [('A', 'B'), ('A', 'C'), ('B', 'C')]
```
<br>

#### 중복 순열
product는 permutations와 같이 리스트와 같은 iterable 객체에서 r개의 데이터를 뽑아 일렬로 나열하는 모든 경우(순열)을 계산한다. 다만 원소를 중복하여 뽑는다.  
쉽게 생각하면, 순열은 하나의 리스트에서 원소를 뽑고 나머지에 대해서 다음 원소를 뽑았다면, 중복 순열은 리스트에서 하나의 원소를 뽑고 기억한뒤 다시 그 원소를 넣어 원래 리스트를 만들고 다시 뽑는 행위와 같다.  
이를 데카르트 곱이라고 한다.(A X A)  
```python
from itertools import product
data = ['A','B','C']
result = list(product(data,repeat=2)) # data X data
print(result)
# [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'A'), ('B', 'B'), ('B', 'C'), ('C', 'A'), ('C', 'B'), ('C', 'C')]
```

<br>

product를 조금 더 활용해보자.  
그렇다면 repeat옵션을 주지 않는다면 어떻게 될까?
```python
print(list(product((0,1))))
# [(0,), (1,)]
```
repeat 옵션이 들어가지 않으면 기본값으로 1이 적용된다.  
그렇다면 (0,1)과 데카르트 곱을 할 대상이 없는 것이다.  
따라서 위와 같은 결과값이 나온다.  
반면에 아래의 경우는 데카르트 곱의 대상이 있기 때문에 정상적인 결과값이 나온다.  
```python
print(list(product((0,1),(2,3))))
# [(0, 2), (0, 3), (1, 2), (1, 3)]
```
<br>

그렇다면 repeat 옵션을 줘보자.
```python
print(list(product((0,1),(2,3),repeat=2)))
# [(0, 2, 0, 2), (0, 2, 0, 3), (0, 2, 1, 2), (0, 2, 1, 3), (0, 3, 0, 2), (0, 3, 0, 3), (0, 3, 1, 2), (0, 3, 1, 3), (1, 2, 0, 2), (1, 2, 0, 3), (1, 2, 1, 2), (1, 2, 1, 3), (1, 3, 0, 2), (1, 3, 0, 3), (1, 3, 1, 2), (1, 3, 1, 3)]
```
이건 무슨 뜻일까?  
위 코드를 해석하면 다음과 같다.
```python
print(list(product((0,1),(2,3),(0,1),(2,3))))
```
(0,1),(2,3)을 한번 더 만들어서 데카르트 곱을 하겠다는 뜻이다.  
<Br>

참고로 위와는 별개로 만약 중복 순열에서 해당하는 문자에 특정 개수만을 중복하도록 주어주려면, 리스트에 일단 모든 개수만큼 담아놓고 permutation을 이용한 뒤 set으로 중복을 제거하는 방법이 있다것도 기억해두자.  


<br>

#### 중복 조합
combinations_with_replacement는 combinations와 같이 리스트와 같은 iterable 객체에서 r개의 데이터를 뽑아 순서를 고려하지 않고 나열하는 모든 경우(조합)을 계산한다. 다만 원소를 중복해서 뽑는다. 마찬가지로 클래스이므로 초기화 후에 __리스트 자료형__ 으로 변환하여 사용해야 한다. 리스트 ['A' , 'B' , 'C']에서 중복을 포함하여 2개를 뽑아 순서에 상관없이 나열하는 모든 경우를 출력하면 다음과 같다.  
```python
from itertools import combinations_with_replacement
data = ['A','B','C']
result = list(combinations_with_replacement(data,2))
print(result)
# [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'B'), ('B', 'C'), ('C', 'C')]
```

<Br>

#### chain
chain은 배열을 한번에 이어붙일 수 있는 기능을 제공한다.
```python
from itertools import chain

a = [[1,2,3],[4,5,6],[7,8,9]]

b = list(chain(*a))
print(b) # [1, 2, 3, 4, 5, 6, 7, 8, 9]

a = [1,2,3]
b = [4,5,6]
c = [7,8,9]
d = list(chain(a,b,c))
print(d) # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### heapq
파이썬에서는 힙 기능을 위해 heapq 라이브러리를 제공한다. heapq는 다익스트라 최단 경로 알고리즘을 포함해 다양한 알고리즘에서 우선순위 큐 기능을 구현하고자 할 때 사용한다. heapq 외에도 PriorityQueue 라이브러리를 사용할 수 있지만, 코딩 테스트 환경에서는 보통 heapq가 더 빠르게 동작하므로 heapq를 사용하자.  
파이썬의 힙은 __최소 힙__ 으로 구성되어 있으므로 단순히 원소를 힙에 전부 넣었다가 빼는 것만으로도 시간 복잡도 O(NlogN)에 오름차순 정렬이 완료된다. 보통 최소 힙 자료구조의 최상단 원소는 항상 가장 작은 원소이기 때문이다.  
```python
import heapq

def heapsort(iterable):
    h=[]
    result=[]
    for value in iterable:
        heapq.heappush(h,value)
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result

result = heapsort([1,3,5,7,9,2,4,6,8,0])
print(result)
# [0,1,2,3,4,5,6,7,8,9]
```
또한 파이썬에서는 최대 힙을 제공하지 않는다. 따라서 heapq 라이브러리를 이용하여 최대 힙을 구현해야 할 때는 원소의 부호를 임시로 변경하는 방식을 사용한다. 힙에 원소를 삽입하기 전에 잠시 부호를 반대로 바꾸었다가, 힙에서 원소를 꺼낸 뒤에 다시 원소의 부호를 바꾸면 된다.  
```python
import heapq

def heapsort(iterable):
    h=[]
    result=[]
    for value in iterable:
        heapq.heappush(h,-value)
    for i in range(len(h)):
        result.append(-heapq.heappop(h))
    return result

result = heapsort([1,3,5,7,9,2,4,6,8,0])
print(result)
# [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

### bisect
파이썬에서는 이진 탐색을 쉽게 구현할 수 있도록 bisect 라이브러리를 제공한다. bisect 라이브러리는 '정렬된 배열'에서 특정한 원소를 찾아야 할 때 매우 효과적으로 사용된다. bisect 라이브러리에서는 bisect_left()와 bisect_right() 함수가 가장 중요하게 사용되며, 시간 복잡도는 O(logN) 이다.  
+ bisect_left(a,x) : 정렬된 순서를 유지하면서 리스트 a에 데이터 x를 삽입할 가장 왼쪽 인덱스를 찾는 함수
+ bisect_right(a,x) : 정렬된 순서를 유지하면서 리스트 a에 데이터 x를 삽입할 가장 오른쪽 인덱스를 찾는 함수

예를 들어 정렬된 리스트 [1,2,4,4,8]이 있을 때 4를 삽입하려고 한다면 left는 2를 right는 4를 반환한다.  
```python
from bisect import bisect_left,bisect_right

a = [1,2,4,4,8]
x = 4
print(bisect_left(a,4)) # 2
print(bisect_right(a,4)) # 4
```
<br>

bisect_left()와 bisect_right()는 정렬된 리스트에서 값이 특정 범위에 속하는 원소의 개수를 구하고자 할 때, 효과적으로 사용할 수 있다.  
```python
from bisect import bisect_left,bisect_right
# 정렬된 리스트에서 값이 [left_value,right_value]에 속하는 데이터의 개수를 반환
# bisect_right이 제일 오른쪽을 반환하므로 right_value도 포함된다. 
def count_by_range(a,left_value,right_value):
    right_index = bisect_right(a,right_value)
    left_index = bisect_left(a,left_value)
    return right_index-left_index
a = [1,2,3,3,3,4,4,8,9]

# 값이 4인 데이터 개수 출력
print(count_by_range(a,4,4)) # 2

# 값이 [-1,3] 범위에 있는 데이터 개수 출력
print(count_by_range(a,-1,3)) # 5
```

### collections
collections 라이브러리 기능 중에 코딩 테스트에서 유용하게 사용되는 클래스는 deque와 Counter이다.  
보통 파이썬에서는 deque를 사용해 큐를 구현한다. deque에서는 리스트 자료형과 다르게 인덱싱, 슬라이싱 등의 기능은 사용할 수 없다. 다만, 연속적으로 나열된 데이터의 시작 부분이나 끝부분에 데이터를 삽입하거나 삭제할 때는 매우 효과적으로 사용할 수 있다. deque는 스택이나 큐의 기능을 모두 포함한다고 볼 수 있기 때문에 스택 혹은 큐 자료구조의 대용으로 사용될 수 있다.  
첫 번째 원소를 제거할 때 popleft(), 마지막 원소를 제거할 때 pop(), 첫 번째 인덱스에 원소 x를 삽입할 때 appendleft(x), 마지막 인덱스에 원소를 삽일할 때 append(x)를 사용한다.  
따라서 deque를 큐 자료구조로 사용할 때, 원소 삽입은 append()를 사용하고 삭제는 popleft()를 사용한다. 그러면 먼저 들어온 원소가 항상 먼저 나가게 된다.  
```python
from collections import deque
data = deque([2,3,4])
data.append(5)
data.popleft()
print(data) # deque([3, 4, 5])
print(list(data)) # [3, 4, 5]
```
<br>

파이썬 collections 라이브러리의 Counter는 등장 횟수를 세는 기능을 제공한다. 구체적으로 리스트와 같은 iterable 객체가 주어졌을 때, 해당 객체 내부의 원소가 몇 번씩 등장했는지를 알려준다.  
```python
from collections import Counter
counter = Counter(['red','blue','green','blue','red'])
print(counter['red']) # 2
print(counter['green']) # 1
print(dict(counter)) # {'red': 2, 'blue': 2, 'green': 1}
```
<br>

### math
math 라이브러리는 자주 사용하는 수학적인 기능을 포함하고 있는 라이브러리이다. 팩토리얼, 제곱근, 최대공약수 등을 계산하는 기능을 포함하고 있다.  
```python
import math
print(math.factorial(5)) # 120
print(math.sqrt(9)) # 3.0
print(math.gcd(21,14)) # 7
print(math.pi)
print(math.e) # 자연상수 e
```
<Br>

## 3. 외부 라이브러리
---
### numpy
numpy는 백준에서는 사용하지 못하지만 프로그래머스에서는 사용 가능하니 상황에 맞게 잘 써야한다.  

#### 행렬 전환 array
```python
import numpy as np

a =[[1, 2, 3, 4, 5],[6, 7, 8, 9, 10],[11, 12, 13, 14, 15]]
array = np.array(a)
print(array)
# [[ 1  2  3  4  5]
#  [ 6  7  8  9 10]
#  [11 12 13 14 15]]
```
배열을 인자로 array 함수에 넣으면 행렬이 된다.

#### 사직연산
```python
import numpy as np

a =[[1, 2, 3, 4, 5],[6, 7, 8, 9, 10],[11, 12, 13, 14, 15]]
b =[[1, 2, 3, 4, 5],[6, 7, 8, 9, 10],[11, 12, 13, 14, 15]]
array1 = np.array(a)
array2 = np.array(b)

print(array1+array2)
print(array1-array2)
print(array1//array2)
print(array1%array2)
print(array1/array2)
print(array1*array2)
```
배열과 다르게 사칙연산이 가능하다.

#### min,max
```python
import numpy as np

a =[[1, 2, 3, 4, 5],[6, 7, 8, 9, 10],[11, 12, 13, 14, 15]]
array = np.array(a)
print(array.max()) # 15
print(array.min()) # 1

# 열 별로 최대값
print(array.max(axis=0)) # [11 12 13 14 15]

# 행별로 최대값
print(array.max(axis=1)) # [ 5 10 15]
```

#### 크기
```python
a =[[1, 2, 3, 4, 5],[6, 7, 8, 9, 10],[11, 12, 13, 14, 15]]
array = np.array(a)
print(array.shape) # (3, 5)
```
행렬의 크기를 튜플 형태로 확인합니다.

#### 인덱싱
```python
import numpy as np

a =[[1, 2, 3, 4, 5],[6, 7, 8, 9, 10],[11, 12, 13, 14, 15]]
array = np.array(a)
print(array[:,1:3]) # 행 전체, 열은 1:3 슬라이싱
# [[ 2  3]
#  [ 7  8]
# [12 13]]

print(array[:2, 1:3]) # 행은 :2, 열은 1:3 슬라이싱
# [[2 3]
#  [7 8]]
```
배열에서는 할 수 없는 간편한 2차원 인덱싱을 제공한다.  
__인덱싱이 괄호 기준이 아니라 쉼표를 기준으로 나누므로 주의해야한다.__

#### all, any
```python
import numpy as np

a=[[0,0],[0,0]]
b=[[0,1],[0,0]]
array1 = np.array(a)
array2 = np.array(b)
print(array1.all()) # False
print(array1.any()) # False
print(array2.all()) # False
print(array2.any()) # True

# 조건식 활용
print(np.all(array1==0)) # True
print(np.any(array1==0)) # True
print(np.all(array2==1)) # False
print(np.any(array1==1)) # False
```
any은 행렬 중 하나라도 참이면 true, all은 행렬 중 모두 참으로 이뤄져 있어야만 true를 반환한다.  

#### list로 되돌리기
```python
import numpy as np

a=[[0,0],[0,0]]
array = np.array(a)
a = array.tolist()
print(a) # [[0, 0], [0, 0]]
```



---
__본 포스팅은 '이것이 코딩 테스트다 with 파이썬'을 읽고 공부한 내용을 바탕으로 작성하였습니다.__