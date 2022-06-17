---
layout: post
title: 그래프 이론 기출문제
subtitle:   그래프 이론 기출문제
categories: algorithm
tags: algorithm-intermediate
comments: true
# header-img:
---
* 
{:toc}


## 1. 간단 정리
---
### 서로소 집합
서로소 집합은 공통 원소가 없는 두 집합이다. 이때 집합 간의 관계를 파악하기 위해서 서로소 집합 알고리즘을 사용할 수 있다. 서로소 집합 알고리즘은 union - find 연산으로 구성되며, 모든 노드는 자신이 속한 집합을 찾을 때 루트 노드를 재귀적으로 찾는다. 서로소 집합 알고리즘은 최소 신장 트리를 찾는 크루스칼 알고리즘에서 사용되기도 한다.
<br>

### 신장 트리
신장 트리는 하나의 그래프가 있을 때 모든 노드를 포함하는 부분 그래프를 의미한다. 일반적으로 코딩테스트에서는 최소 신장 트리 문제가 출제된다.

### 크루스칼 알고리즘
크루스칼 알고리즘은 가능한 최소 비용의 신장 트리를 찾아주는 알고리즘이다. 시간 복잡도는 O(ElogE)로 간선을 정렬한 뒤에 간선의 비용이 작은 순서대로 차례대로 최소 신장 트리를 만들어 가는 그리디 알고리즘의 일종이다.

### 위상 정렬 알고리즘
위상 정렬 알고리즘은 방향 그래프의 모든 노드들을 방향성에 거스르지 않도록 순서대로 나열한 정렬 기법이다. 예를 들어 선수과목을 고려한 학습 순서 설정 문제 등에서 사용될 수 있다. 큐 자료구조를 이용한 위상 정렬의 시간 복잡도는 O(V+E)이다.  
<br>

서로소 집합 알고리즘과 최소 신장 트리 알고리즘은 종종 코딩테스트에서 출제되는 알고리즘 유형이며, 위상 정렬 알고리즘은 난이도가 높은 후반부 문제에서 가끔 출제되므로 기억해두자.  

<br>

## 2. 여행 계획
---
주인공이 사는 나라에는 N개의 여행지가 있으며, 각 여행지는 1 ~ N번까지의 번호로 구분된다. 또한 임의의 두 여행지 사이에는 두 여행지를 연결하는 도로가 존재할 수 있다. 이때, 여행지가 도로로 연결되어 있다면 양방향으로 이동이 가능하다는 의미이다. 주인공은 하나의 여행 계획을 세운 뒤에 이 여행 계획이 가능한지의 여부를 판단하고자 한다. 여행지의 개수와 여행지 간의 연결 정보가 주어졌을 때, 주인공의 여행 계획이 가능한지 여부를 판별하는 프로그램을 작성하시오.  
__입력 조건__  
+ 첫째 줄에 여행지의 수 N과 여행 계획에 속한 도시의 수 M이 주어진다. (1<= N,M <=500)
+ 다음 N개의 줄에 걸쳐 N * N 행렬을 통해 임의의 두 여행지가 서로 연결되어 있는지의 여부가 주어진다. 그 값이 1이라면 서로 연결되었다는 의미이며, 0이라면 서로 연결되지 않았다는 의미이다.
+ 마지막 줄에 주인공의 여행 계획에 포함된 여행지 번호들이 주어지며 공백으로 구분한다.

__출력 조건__  
+ 첫째 줄에 주인공의 여행 계획이 가능하다면 yes, 불가능시 no출력

```
입력 예시
5 4
0 1 0 1 1
1 0 1 1 0
0 1 0 0 0
1 1 0 0 0
1 0 0 0 0
2 3 4 3

출력예시
yes
```


### 내가 작성한 코드
```python
def findParent(parent, idx):
    if parent[idx] != idx:
        parent[idx] = findParent(parent, parent[idx])
    return parent[idx]


def union(parent, idx1, idx2):
    a = findParent(parent, idx1)
    b = findParent(parent, idx2)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b


n, m = map(int, input().split())
parent = [0] * (n)

graph = [[] for _ in range(n)]
for i in range(n):
    graph[i] = list(map(int, input().split()))

plan = list(map(int, input().split()))

# 여행 위치에 대한 union 작업
for idx in plan:
    for i in range(n):
        if graph[idx][i] == 1:
            union(parent, idx, i)

ans = parent[plan[0]]
key = 1
for idx in plan[1:]:
    if parent[idx] != ans:
        key = 0
        break

if key:
    print('yes')
else:
    print('no')

```
서로소 집합 알고리즘을 이용하여, 그래프에서 노드간의 연결성을 파악해 해결할 수 있다. 즉, 여행 계획에 해당하는 모든 노드가 같은 집합에 속하면 가능한 여행 경로 라는 것이다.

### 모범 답안
```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

# 여행지의 개수와 여행 계획에 속한 여행지의 개수 입력받기
n, m = map(int, input().split())
parent = [0] * (n + 1) # 부모 테이블 초기화

# 부모 테이블상에서, 부모를 자기 자신으로 초기화
for i in range(1, n + 1):
    parent[i] = i

# Union 연산을 각각 수행
for i in range(n):
    data = list(map(int, input().split()))
    for j in range(n):
        if data[j] == 1: # 연결된 경우 합집합(Union) 연산 수행
            union_parent(parent, i + 1, j + 1)

# 여행 계획 입력받기
plan = list(map(int, input().split()))

result = True
# 여행 계획에 속하는 모든 노드의 루트가 동일한지 확인
for i in range(m - 1):
    if find_parent(parent, plan[i]) != find_parent(parent, plan[i + 1]):
        result = False

# 여행 계획에 속하는 모든 노드가 서로 연결되어 있는지(루트가 동일한지) 확인
if result:
    print("YES")
else:
    print("NO")
```
union한 이후에는 그래프의 정보를 저장해야할 필요가 없기 때문에 한 줄씩 그래프 정보를 받고 처리한 후에 다시 다음 그래프 정보로 덮어씌운다는 점이 내 코드랑 다른 점이다. 이렇게 하면 메모리를 조금이나마 아낄 수 있다.

<br>

## 3. 탑승구
---
공항에는 G개의 탑승구가 있으며, 각각 탑승구는 1번부터 G번까지의 번호로 구분된다. 공항에는 P개의 비행기가 차례대로 도착할 예정이며, i번째 비행기를 1번부터 g번째 탑승구 중 하나에 영구적으로 도킹해야한다. 이때, 다른 비행기가 도킹하지 않은 탑승구에만 도킹할 수 있다.  
또한 P개의 비행기를 순서대로 도킹하다가 만약에 어떤 탑승구에 도킹할 수 없는 비행기가 나오는 경우, 그 시점에서 공항의 운행을 중지시킨다. 공항의 관리자는 최대항 많은 비행기를 공항에 도킹하고자 한다. 비행기를 최대 몇 대 도킹할 수 있는지 출력하는 프로그램을 작성하시오.  
__입력 조건__  
+ 첫째 줄에는 탑승구의 수 G(1<=G<=100,000)
+ 둘째 줄에는 비행기의 수 P(1<=P<=100,000)
+ 다음 P개의 줄에는 각 비행기가 도킹할 수 있는 탑승구의 정보 G(1<=P<=G)가 주어진다. 이는 i 번째 비행기가 1번부터 G번째 탑승구 중 하나에 도킹할 수 있다는 의미이다.

__출력 조건__  
+ 첫째 줄에 도킹할 수 있는 비행기의 최대 개수를 출력

```
입력 예시
4
3
4
1
1

출력 예시
2

입력 예시
4
6
2
2
3
3
4
4

출력 예시
3
```

### 내가 작성한 코드
```python
g = int(input())
p = int(input())


def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]


def union(parent, x, y):
    a = find_parent(parent, x)
    b = find_parent(parent, y)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b


# 부모는 자기 자신
parent = [0] * (g + 1)
for i in range(g + 1):
    parent[i] = i

# 도커 정보
docks=[]
for i in range(p):
    docks.append(int(input()))


cnt = 0
for dock in docks:
    pos_dock = find_parent(parent, dock)
    if pos_dock==0:
        break
    union(parent, pos_dock, pos_dock - 1)
    cnt += 1

print(cnt)
```
주어진 탑승구중 가장 마지막 게이트에 도킹하는게 가장 합리적이다.  
마지막이 아니라 앞쪽에다가 도킹 시 적은 범위의 비행기가 들어왔을때 앞선 비행기가 뒤쪽에 도킹이 가능했는데도 중단해야 되기 때문이다.  
그렇다면 만약 충돌이 일어난다면 앞쪽에 도킹을 해야하는데 일일이 하나씩 앞쪽에 자리가 비었는지 확인하는 건 복잡도가 너무 크다.  
한번에 비어있는 자리를 찾을 수 있도록 알고리즘을 생각해야 한다.  
find union 알고리즘은 기본적으로 한 집합에서 가장 작은 숫자를 대표로 보고 있다.  
이를 활용하면 어느 자리가 비었는지 한번에 파악할 수 있다.  

### 모범 답안
이 문제는 서로소 집합 알고리즘을 이용하면 쉽게 해결할 수 있다. 각 탑승구를 서로 다른 집합으로 나타낸다고 해보자. 전체 탑승구가 4개라고 가정하면 각각 parent는 자신의 탑승구 번호를 가리킨다. 이때 비행기가 순서대로 들어오면 차례대로 도킹을 수행해야 하는데, 가능한 큰 번호의 탑승구로 토킹을 우선 시행해야한다. 이때 도킹하는 과정을 탑승구 간 union 연산으로 이해할 수 있다. 새롭게 도킹이 되면, 해당 집합은 바로 왼쪽에 있는 집합과 합친다. 단, 집합의 루트가 0이되면 더이상 도킹이 불가능 한것으로 판단한다. 
```python
import sys

input = sys.stdin.readline


def find_parent(x):
    if parent[x] != x:
        parent[x] = find_parent(parent[x])
    return parent[x]


def union(x, y):
    a = find_parent(x)
    b = find_parent(y)
    if a > b:
        parent[a] = b
    else:
        parent[b] = a


# 탑승구 수, 비행기 수
g = int(input())
p = int(input())
parent = [0] * (g + 1)
cnt = 0
limit = []
# 집합 설정
for i in range(g + 1):
    parent[i] = i

for _ in range(p):
    limit.append(int(input()))

for i in limit:
    # 더이상 불가
    if find_parent(i) == 0:
        break
    # 자기 자신이면
    if find_parent(i) == i:
        union(i, i - 1)

    else:
        a = find_parent(i)
        union(a, a - 1)
    cnt += 1

print(cnt)
```
<br>

## 4. 어두운 길
---
한 마을은 N개의 집과 M개의 도로로 구성되어 있다. 각 집은 0번부터 N-1번까지의 번호로 구분된다. 모든 도로에는 가로등이 구비되어 있는데, 특정한 도로의 가로등을 하루 동안 켜기 위한 비용을 해당 도로의 길이와 동일하다. 예를 들어 2,3번 집 사이를 연결하는 길이가 7인 도로가 있다면 하루 종일 켜두는 비용은 7이다.  
정부에서 일부 가로등을 비활성화하되, 마을에 있는 임의의 두 집에 대하여 가로등이 켜진 도로만으로도 오갈 수 있도록 만들고자 한다. 결과적으로 일부 가로등을 비활성화하여 최대한 많은 금액을 절약하고자 한다. 마을의 집과 도로 정보가 주어졌을 때, 가로등을 비활성화하여 절약할 수 있는 최대 금액을 출력하는 프로그램을 작성하시오.  
__입력 조건__  
+ 첫째 줄에 집의 수 N(1<=N<=200,000)과 도로의 수 M(N-1<=M<=200,000)이 주어진다.
+ 다음 M개의 줄에 걸쳐서 각 도로에 대한 정보 X,Y,Z가 주어지며, 공백으로 구분한다. (0<=X,Y < N ) 이는 X번 집과 Y번 집 사이에 양방향 도로가 있으며, 그 길이가 Z라는 의미이다. 단 x,y가 동일한 경우는 없으며 마을을 구성하는 모든 도로의 길이 합은 2^31보다 작다.

__출력 조건__  
+ 첫째 줄에 일부 가로등을 비활성화하여 절약할 수 있는 최대 금액을 출력

```
입력 예시
7 11
0 1 7
0 3 5
1 2 8
1 3 9
1 4 7
2 4 5
3 4 15 
3 5 6
4 5 8
4 6 9
5 6 11

출력 예시
51
```
### 내가 작성한 코드
전형적인 최소 신장 트리 문제이므로 크루스칼 알고리즘을 사용해 해결했다.  
비용을 기준으로 좌표와 함께 정렬하고 union작업을 했다. 부모가 같다면 이미 연결되어있으므로 union작업을 하지 않고 절약 비용에 추가했다. 
```python
import sys
import heapq

def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]


def union(parent, x, y):
    a = find_parent(parent, x)
    b = find_parent(parent, y)
    if a > b:
        parent[a] = b
    else:
        parent[b] = a

def kruscal(q,parent):
    ans =0
    while q:
        z,x,y = heapq.heappop(q)
        if find_parent(parent,x) != find_parent(parent,y):
            union(parent,x,y)
        else:
            ans+=z

    return ans

input = sys.stdin.readline

n,m = map(int,input().split())
q=[]

parent = [0]*n
for i in range(n):
    parent[i]=i

for _ in range(m):
    x,y,z = map(int,input().split())
    heapq.heappush(q,(z,x,y))

print(kruscal(q, parent))
```

<br>

## 5. 행성 터널
---
[문제 클릭](https://www.acmicpc.net/problem/2887){: target="_blank"}  

### 내가 작성한 코드
```python
import heapq
import sys


def findParent(parent, idx):
    if parent[idx] != idx:
        parent[idx] = findParent(parent, parent[idx])
    return parent[idx]


def union(parent, idx1, idx2):
    a = findParent(parent, idx1)
    b = findParent(parent, idx2)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b


def kruscal(edges, parent):
    ans = 0
    while edges:
        cost, idx1, idx2 = heapq.heappop(edges)
        if findParent(parent, idx1) != findParent(parent, idx2):
            union(parent, idx1, idx2)
            ans += cost

    return ans


input = sys.stdin.readline

n = int(input())
graph = []
edges = []

parent = [0] * (n)
for i in range(n):
    parent[i] = i

for idx in range(n):
    tmp = list(map(int, input().split()))
    tmp.append(idx)
    graph.append(tmp)

# 3방향 최소값 간선
for i in range(3):
    graph.sort(key=lambda x: x[i])
    for idx in range(n - 1):
        # 비용과 양쪽 정점 인덱스
        heapq.heappush(edges, (graph[idx + 1][i] - graph[idx][i], graph[idx][3], graph[idx + 1][3]))

print(kruscal(edges, parent))
```
문제의 조건을 잘 봐야 한다. 처음에 문제를 잘못 읽어 거리 공식인 제곱으로 빼는 식인줄 알았다..  
연결하는데 최소 비용을 구하는 것이므로 당연히 크루스칼 알고리즘을 생각해냈다.  
크루스칼알고리즘을 사용하기 위해서는 간선정보와 인덱스 정보를 알아야 한다.  
3방향 좌표이지만 입력 순서에 따라 인덱스를 먹여주면 되기 때문에 인덱스는 해결할 수 있다.  
그렇다면 남은 것은 간선정보인데 모든 정점에 대해 각각의 정점에 대한 간선을 구하는 방식은 N의 개수가 100,000개이므로 복잡도가 너무 크다.  
여기서는 연결 비용을 구하는 식이 힌트를 주고 있다.  
각 x,y,z 좌표간의 차이 중 최소값이 연결에 드는 비용이므로 각 좌표를 정렬해서 x끼리의 간선정보, y끼리의 간선정보, z끼리의 간선정보를 구하면 총 3(n-1)개의 간선정보를 구할 수 있다.  
이는 최대 30만개이므로 충분히 연산할 수 있는 정도이다.  


### 모범 답안
이 문제는 n - 1개의 터널을 설치해서 모든 행성이 연결되도록 요구하므로, 최소 신장 트리를 만드는 문제로 이해할 수 있다. 여기서 당연히 크루스칼 알고리즘을 생각해 낼 것이다. 하지만 여기서 주의해야 한다. 크루스칼 알고리즘은 정렬하는 부분이 가장 많은 복잡도를 소요하므로 (ElogE)이다. 그런데 이 문제에서는 임의의 두 노드 사이에 터널을 연결할 수 있다고 가정하고 있다. 따라서 간선의 개수가 n-1, n-2, n-3 ... 1 개가 생성되어 간선의 총 개수가 N(N-1)/2이다. N의 범위가 100,000까지이므로 간선의 개수가 매우 커져 시간 안에 해결할 수 없다.  
하지만 터널 비용의 정의를 이용하면 간선의 개수를 줄일 수 있다. 입력 받은 x,y,z축을 기준으로 각각 정렬을 수행한다. x축만 고려해서 예시를 들어보면, 주어진 예시를 정렬시 -1,10,11,14,19로 정렬 될 것이다. 그렇다면 차례대로 간선을 만들어 주면 n-1개가 생기게 된다.  
여기서 살짝 이해가 안될 수 있다. 생각해보자. 지금 문제 조건은 최소 거리로 터널을 만드는 것이다. 그렇다면 현재 행성에서 최소 거리에 있는 거리만 고려하면 된다는 것이다. -1과 10을 간선으로 연결하지 않고 -1과 11을 연결하면 그 비용이 더 커진다. 따라서 인접한 것 끼리만 간선을 만들어 주는 것이다.  
결과적으로 계속 진행하면 축마다 n-1개의 간선이 생기므로 총 3 * (n-1)개의 간선이 생기고 이를 크루스칼 알고리즘을 수행하면 시간 안에 해결할 수 있다.  

```python
import sys

input = sys.stdin.readline # 입력이 매우 많으므로


def find_parent(x):
    if parent[x] != x:
        parent[x] = find_parent(parent[x])
    return parent[x]


def union(x, y):
    a = find_parent(x)
    b = find_parent(y)
    if a > b:
        parent[a] = b
    else:
        parent[b] = a


n = int(input())
x = []
y = []
z = []
parent = [0] * (n + 1)

# 처음 parent 초기화
for i in range(1, n + 1):
    parent[i] = i

# 좌표별로 삽입
for i in range(1, n + 1):
    a, b, c = map(int, input().split())
    x.append((a, i))
    y.append((b, i))
    z.append((c, i))

x.sort()
y.sort()
z.sort()

# 간선 정보 담을 곳
answer = []

# 간선 담기
# 간선의 개수는 n-1개이므로 
for i in range(n - 1):
    answer.append((x[i + 1][0] - x[i][0], x[i][1], x[i + 1][1]))
    answer.append((y[i + 1][0] - y[i][0], y[i][1], y[i + 1][1]))
    answer.append((z[i + 1][0] - z[i][0], z[i][1], z[i + 1][1]))

answer.sort()
total = 0
for cost, x, y in answer:
    if find_parent(x) != find_parent(y):
        union(x, y)
        total += cost
print(total)
```
<br>

## 6. 최종 순위
---
[문제 클릭](https://www.acmicpc.net/problem/3665){: target="_blank"}  

### 내가 작성한 코드
문제에서 약간 혼동되게 작성되있는 부분이 있다. 상대적 순위 변동 시, (6,13)으로 주어져 있는데 이건 6이 순위가 더 높아졌다는 뜻이 아니라, 팀6과 팀 13의 상대적 순위에 변동이 있다는 의미이고 작은 수부터 앞에 작성한다는 뜻이다.  
```python
from collections import deque


def topoloySort(graph, in_cnt):
    q = deque()
    ans = []
    # 진입차수 0인것 삽입
    for idx in range(1, n + 1):
        if in_cnt[idx] == 0:
            q.append(idx)

    # 큐에서 n개의 노드를 뽑아야 순위가 완성됨
    for i in range(n):
        if len(q) == 0:
            print("IMPOSSIBLE")
            return

        # 큐에 2개 이상 담겨있다면 들어오는 순서에 따라 정렬 순서가 바뀌므로 확실한 순위를 찾을 수 없음
        if len(q) > 1:
            print("?")
            return

        idx = q.popleft()
        ans.append(idx)

        # 연결된 정점의 차수 제거와 0인경우 큐삽입
        for j in range(1, n + 1):
            if graph[idx][j] == 1:
                in_cnt[j] -= 1
                if in_cnt[j] == 0:
                    q.append(j)

    print(*ans)


t = int(input())

for _ in range(t):
    n = int(input())
    graph = [[0] * (n + 1) for _ in range(n + 1)]
    in_cnt = [0] * (n + 1)

    before = list(map(int, input().split()))

    # 인접 행렬 만들기
    for i in range(n):
        in_cnt[before[i]] = i
        for j in range(i + 1, n):
            graph[before[i]][before[j]] = 1

    m = int(input())
    for _ in range(m):
        a, b = map(int, input().split())
        # 간선 방향 바꾸기
        if graph[a][b] == 1:
            graph[a][b] = 0
            graph[b][a] = 1
            in_cnt[b] -= 1
            in_cnt[a] += 1
        else:
            graph[a][b] = 1
            graph[b][a] = 0
            in_cnt[b] += 1
            in_cnt[a] -= 1

    topoloySort(graph, in_cnt)

```
전체의 순서를 구하는 것이기 때문에 바로 위상정렬 알고리즘을 생각해냈다.  
진입 차수를 0인것을 1등의 시작한다면 진행하면 큐에서 뽑는 순서대로 순위를 정할 수 있다.
하지만 기존의 위상정렬과는 다르게 그래프가 주어진 이후에 그래프의 간선정보가 변경된다.  
기존의 위상정렬 문제에서는 간선들을 연결리스트로 구현했는데 위 문제를 연결리스트로 구현할 경우, 바뀌는 간선들을 지우고 추가해야하기 때문에 복잡도가 커진다.  
즉, 위상 정렬에서 그래프의 간선 정보가 바뀌게 되는 경우에는 연결리스트가 아니라 인접행렬로 구현해야 한다.  
간선 리스트로 풀이를 진행하는 문제는 [커리큘럼 문제(위상정렬)](https://backtony.github.io/algorithm/2020-09-09-algorithm-basics-coding-11/#%EB%AC%B8%EC%A0%9C--%EC%BB%A4%EB%A6%AC%ED%81%98%EB%9F%BC){: target="_blank"}를 참고하자.  
위상정렬 알고리즘에서는 큐에 진입차수가 0인 정점이 담기기 때문에 특별한 문제가 없다면 모든 정점이 한번씩 큐에 들어가게 된다.  
이 점을 생각하면 다음과 같은 로직을 생각할 수 있다.  
+ 주어진 정점의 순위를 정확하게 판단할 수 있다면 큐에서 정점을 빼는 과정은 총 정점의 개수만큼 진행된다.
+ 정점의 개수만큼 진행되기 전에 큐기 비어있다면, 싸이클이 발생한 것으로 순위를 찾을 수 없다.
+ 정점의 개수만큼 진행되는 도중에 큐에 2개 이상의 값이 들어가게 된다면 큐에 들어오는 순서에 따라 순위가 바뀌게 되므로 확실한 순위를 보장할 수 없다.

### 모범 답안
문제에서는 작년 순위와 상대적으로 순위가 바뀐 팀들의 목록이 주어졌을 때, 올해 순위를 만들 것을 요구하고 있다. 즉, __정해진 우선순위에 맞게 전체 팀들의 순서를 나열한다(선수과목)__ 는 점에서 위상 정렬 알고리즘을 떠올릴 수 있어야 한다.  
다시 말해 이 문제는 팀 간의 순위 정보를 그래프 정보로 표현한 뒤에, 위상 정렬 알고리즘을 이용해 해결할 수 있다. 주어진 예시를 가지고 생각해보자. 작년 순위 정보를 기준으로하여 __자기보다 낮은 등수를 가진 팀을 가리키토록 방향 그래프__ 를 만들 수 있다. 즉, 1등팀인 팀5는 1,2,3,4로 방향을 가리킬 수 있는 것이다. 이대로 위상 정렬을 수행하게 되면, 수행 결과는 5-4-3-2-1로 나온다.  
상대적인 순위가 바뀌게 되는 경우에는 해당 간선의 방향을 반대로 변경하면 된다. 여기서 위상 정렬을 수행하게 되면 사이클이 발생하는 경우와 위상 정렬의 결과가 1개가 아니라 여러 가지인 경우로 2가지 특이 케이스가 발생한다. 이 2가지 경우에 해당하지 않는다면 위상 정렬을 수행한 결과는 오직 하나의 경우만 존재한다. 즉, 가능한 순위가 하나라는 뜻이다.  
따라서 변경된 상대적 순위를 적용한 이후에, 위상 정렬 알고리즘을 실행하면서 사이클이 발생하는지, 혹은 결과가 여러 가지인지 확인하면 된다. 일반적인 위상 정렬의 경우, 정확히 N개의 노드가 큐에서 출력이 된다. 만약 N번 나오기 전에 큐가 비게 된다면, 사이클이 발생한 것으로 이해할 수 있다. 또한 특정 지점에 2개 이상의 노드가 큐에 한꺼번에 들어갈 때는, 가능한 정렬 결과가 여러 가지라는 의미가 된다. 그러므로 위상 정렬 수행 과정에서 큐에서 노드를 뽀을 때 큐의 원소가 항상 1개로 유지되는 경우에만 고유한 순위가 존재하는 것으로 이해할 수 있다. 따라서, 위상 정렬 코드에 매 시점마다 큐의 원소가 0개이거나 2개 이상인지 체크하는 부분을 넣어주면 된다.  

```python
import sys
from collections import deque

input = sys.stdin.readline

def topology_sort(count_graph, link_graph, n):
    answer=[]
    q = deque()
    # 진입차수가 0인 것 큐에 삽입
    for i in range(1,n+1):
        if count_graph[i]==0:
            q.append(i)

    # 노드의 개수 만큼만 반복
    for i in range(n):
        # 사이클 발생이 발생하면 일관성이 없음
        if len(q) == 0:
            print("IMPOSSIBLE")
            return
        # 2개 이상 들어오면 확실한 순위를 찾을 수 없음
        if len(q) > 1:
            print("?")
            return
        idx = q.popleft()
        answer.append(idx)
        # 연결 관계, 진입차수 수정
        for i in range(1,n+1):
            if link_graph[idx][i]== True:                
                count_graph[i]-=1
                # 사실 여기서 false로 안해줘도 된다.
                # 더이상 사용하지 않기 때문
                link_graph[idx][i] = False
                if count_graph[i]==0:
                    q.append(i)

    return answer

case = int(input())
# 테스트 케이스 만큼 반복
for _ in range(case):
    n = int(input())
    # 작년 순위
    rank = list(map(int, input().rstrip().split()))
    # 진입차수 그래프와 연결 상태 그래프
    count_graph = [0] * (n + 1)
    link_graph = [[False] * (n + 1) for _ in range(n + 1)]
    for i in range(n):
        for j in range(i + 1, n):
            count_graph[rank[j]] += 1
            link_graph[rank[i]][rank[j]] = True

    m = int(input())
    # 순위 뒤집기
    for i in range(m):
        a,b = map(int,input().split())
        if link_graph[a][b]: # 이게 어떤 경우지?
            count_graph[a]+=1
            count_graph[b]-=1
            link_graph[a][b]=False
            link_graph[b][a] = True
        else :
            count_graph[a] -= 1
            count_graph[b] += 1
            link_graph[a][b] = True
            link_graph[b][a] = False

    answer = topology_sort(count_graph,link_graph,n)
    if answer:
        for i in answer:
            print(i,end =" ")
        print()
```


<br><br>

---
__본 포스팅은 '이것이 코딩 테스트다 with 파이썬'을 읽고 공부한 내용을 바탕으로 작성하였습니다.__
