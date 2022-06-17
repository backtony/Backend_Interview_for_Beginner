---
layout: post
title: 최단 경로 기출문제
subtitle:   최단 경로 기출문제
categories: algorithm
tags: algorithm-intermediate
comments: true
# header-img:
---
* 
{:toc}
 

## 1. 간단 정리
---
### 최단 경로 알고리즘
그래프상에서 가장 짧은 결로를 찾는 알고리즘이다. 다익스트라 알고리즘과 플로이드 워셜 알고리즘을 성능, 구현 난이도, 역할에 대하여 비교해보자.

알고리즘 종류|시간복잡도|구현 난이도|역할
---|---|---|---
다익스트라|O(ElogV)|어려운 편|한 지점에서 다른 모든 지점까지의 최단 경로를 계산
플로이드 워셜|O(V^3)|쉬운 편|모든 지점에서 다른 모든 지점까지의 최단 경로를 계산

### 다익스트라 알고리즘
다익스트라 알고리즘은 단계마다 방문하지 않은 노드 중에서 가장 최단 거리가 짧은 노드를 선택한 뒤에 그 노드를 거쳐 가는 경우를 확인하여 최단 거리를 갱신하는 방법이다. 우선순위 큐를 이용하여 소스코드를 작성할 수 있다는 점을 기억하자.

### 플로이드 워셜 알고리즘
플로이드 워셜 알고리즘은 다이나믹 프로그래밍을 이용하여 단계마다 거쳐 가는 노드를 기준으로 최단 거리 테이블을 갱신하는 방식으로 동작한다. 다음 점화식만 제대로 기억해 놓는다면 큰 어려움 없이 구현 가능하다. D(ab) = min(D(ab), D(a(ak)+a(kb)))
<Br>

## 2. 플로이드
---
[문제 클릭](https://www.acmicpc.net/problem/11404){: target="_blank"}  

### 내가 작성한 코드
```python
n = int(input())
m = int(input())

INF = int(1e9)
graph = [[INF] * n for _ in range(n)]

# 각 최소값 대입
for _ in range(m):
    a, b, c = map(int, input().split())
    graph[a - 1][b - 1] = min(graph[a - 1][b - 1], c)

# 자기자신으로 가는 경우 0 초기화
for i in range(n):
    graph[i][i] = 0

# 플로이드
for k in range(n):
    for i in range(n):
        for j in range(n):
            graph[i][j] = min(graph[i][k] + graph[k][j], graph[i][j])

# 이동 불가의 경우 0으로 수정
for i in range(n):
    for j in range(n):
        if graph[i][j] == INF:
            graph[i][j] = 0

# 출력
for i in range(n):
    print(*graph[i])
```
모든 경우에 대한 최소거리를 요구했으므로 플로이드 워셜 알고리즘을 생각해냈고, 범위가 100이므로 사용해도 되는 범위라고 생각했다. 플로이드 워셜 알고리즘 작성하면서 자기 자신으로 가는 경우는 0으로 초기화해줘야 하는 부분을 자꾸 생략하고 넘어가는데 잘 기억해두자. 

### 모범 답안
전형적인 최단 경로 문제이다. 다만 입력 조건에 따르면 시작 도시와 도착 도시를 연결하는 간선이 여러 개일 수 있다는 점을 주의해야 한다. 또한 도시의 개수 n이 100이하의 정수이므로 플로이드 워셜 알고리즘을 이용하는 것이 효과적이다. 
```python
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수 및 간선의 개수를 입력받기
n = int(input())
m = int(input())
# 2차원 리스트(그래프 표현)를 만들고, 모든 값을 무한으로 초기화
graph = [[INF] * (n + 1) for _ in range(n + 1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n + 1):
    for b in range(1, n + 1):
        if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력받아, 그 값으로 초기화
for _ in range(m):
    # A에서 B로 가는 비용은 C라고 설정
    a, b, c = map(int, input().split())
    # 가장 짧은 간선 정보만 저장
    if c < graph[a][b]:
        graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for k in range(1, n + 1):
    for a in range(1, n + 1):
        for b in range(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행된 결과를 출력
for a in range(1, n + 1):
    for b in range(1, n + 1):
        # 도달할 수 없는 경우, 0을 출력
        if graph[a][b] == INF:
            print(0, end=" ")
        # 도달할 수 있는 경우 거리를 출력
        else:
            print(graph[a][b], end=" ")
    print()
```

<br>

## 3. 정확한 순위
---
선생님은 시험을 본 학생 N명의 성적을 분실하고, 성적을 비교한 결과의 일부만을 가지고 있다. 학생 N명의 성적은 모두 다른데, 다음은 6명의 학생에 대하여 6번만 성적을 비교한 결과이다. 
+ 1번 학생의 성적 < 5번 학생의 성적
+ 3번 학생의 성적 < 4번 학생의 성적
+ 4번 학생의 성적 < 2번 학생의 성적
+ 4번 학생의 성적 < 6번 학생의 성적
+ 5번 학생의 성적 < 2번 학생의 성적
+ 5번 학생의 성적 < 4번 학생의 성적

A번 학생의 성적이 B번 학생보다 낮다면 화살표가 A에서 B를 가리키도록 한다고 하자. 위의 주어진대로 그림을 그려보면 유추해서 순위를 정확히 알 수 있는 학생도 있고, 알 수 없는 학생도 있다. 예를 들어 1번 학생은 5번 학생보다 성적이 낮고, 5번 학생은 4번 학생보다 성적이 낮으므로 1번 학생은 4번 학생보다 성적이 낮다. 따라서 1번, 3번, 5번 학생은 모두 4번 학생의 성적보다 낮다고 볼 수 있다. 그리고 4번 학생은 2번 학생과 6번 학생보다 성적이 낮다. 정리하면 4번 학생보다 성적이 낮은 학생은 3명이고, 성적이 높은 학생은 2명이므로 4번 학생의 순위를 정확히 알 수 있다. 하지만 4번 학생을 제외한 학생의 순위를 알 수 없다.  
학생들의 성적을 비교한 결과가 주어질 때, 성적 순위를 정확히 알 수 있는 학생은 몇 명인지 계산하는 프로그램을 작성하시오.  
__입력 조건__  
+ 첫째 줄에 학생들의 수 N(2<=N<=500)과 두 학생의 성적을 비교한 횟수 M(2<=M<=10,000)이 주어진다.
+ 다음 M개의 각 줄에는 두 학생의 성적을 비교한 결과를 나타내는 두 양의 정수 A와 B가 주어진다. 이는 A번 학생의 성적이 B번 학생보다 낮다는 것을 의미한다.

__출력 조건__  
+ 첫째 줄에 성적 순위를 정확히 알 수 있는 학생의 수를 출력

```
입력 예시
6 6
1 5
3 4
4 2
4 6
5 2
5 4

출력 예시
1
```

### 내가 작성한 코드
```python
def floyd(graph, n):
    for i in range(n):
        graph[i][i] = 0

    for k in range(n):
        for i in range(n):
            for j in range(n):
                graph[i][j] = min(graph[i][j], graph[i][k] + graph[k][j])


n, m = map(int, input().split())
INF = (int)(1e9)
graph = [[INF] * n for _ in range(n)]
ans = 0

for _ in range(m):
    a, b = map(int, input().split())
    graph[a - 1][b - 1] = 1

floyd(graph, n)

for i in range(n):
    key = 1
    for j in range(n):
        if graph[i][j] == INF and graph[j][i] == INF:
            key = 0
            break
    if key:
        ans += 1

print(ans)
```
처음 순위라고 했을 때, 위상정렬을 생각했다.  
__위상정렬은 전체 순위를 정할 수 있거나, 전체의 정할 수 없는 그래프를 판별하는 알고리즘이다.__  
하지만 __특정 요소만__ 순위 판별하라는 것을 위상정렬로 판별할 수 없다.  
문제를 보면 __각각의 정점이 모든 정점에 대해 도달 가능하거나 도달 당할 수 있다면 성적 처리가 가능하다__  는 것을 확인할 수 있다.  
그렇다면 모든 정점에 대해 다른 정점으로 이동이 가능한지 판단할 수 있는 알고리즘은 플로이드 워셜 알고리즘이다.

### 모범 답안
이 문제는 최단 경로를 계산하는 문제로 볼 수 있다. 문제에서도 나와 있듯이 학생들의 성적을 비교한 결과를 방향 그래프 형태로 표현할 수 있다. 성적이 낮은 학생이 성적이 높은 학생을 가리키는 방향 그래프로 표현할 수 있으므로, 최단 경로 알고리즘을 수행할 수 있다.  
A번 학생과 B번 학생의 성적을 비교할 때, 경로를 이용하여 성적 비교 결과를 알 수 있다. A에서 B로 도달이 가능하다는 것은, A가 B보다 성적이 낮다는 의미가 된다. 따라서 A에서 B로 도달이 가능하거나 B에서 A로 도달이 가능하면 성적 비교가 가능한 것이다. 즉, 비교 과정 중에 어느 한쪽으로든 도달이 가능하면 성적 비교가 가능한 것이다.  
이 문제에서는 학생의 수 N이 500이하의 정수이므로 O(N^3)인 플로이드 워셜 알고리즘을 이용해 해결할 수 있다.
```python
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 2차원 리스트(그래프 표현)를 만들고, 모든 값을 무한으로 초기화
graph = [[INF] * (n + 1) for _ in range(n + 1)]
 
# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n + 1):
    for b in range(1, n + 1):
        if a == b:
            graph[a][b] = 0
 
# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _ in range(m):
    # A에서 B로 가는 비용을 1로 설정
    a, b = map(int, input().split())
    graph[a][b] = 1
 
# 점화식에 따라 플로이드 워셜 알고리즘을 수행
for k in range(1, n + 1):
    for a in range(1, n + 1):
        for b in range(1, n + 1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

result = 0
# 각 학생을 번호에 따라 한 명씩 확인하며 도달 가능한지 체크
for i in range(1, n + 1):
    count = 0
    for j in range(1, n + 1):
        # 어느 한쪽이든 도달이 가능한 경우 비교가 가능
        if graph[i][j] != INF or graph[j][i] != INF:
            count += 1
    if count == n:
        result += 1
print(result)
```

<br>

## 4. 화성 탐사
---
화성 탐사 기계가 출발 지점에서 목표 지점까지 이동할 때 항상 최적의 경로를 찾도록 개발해야 한다.  
화성 탐사 기계가 존재하는 공간은 N * N 크기의 2차원 공간이며, 각각의 칸을 지나기 위한 비용이 존재한다. 가장 왼쪽 위 칸인 0,0 위치에서 가장 오른쪽 아래 칸인 n-1,n-1 위치로 이동하는 최소 비용을 출력하는 프로그램을 작성하시오. 기계는 상하좌우로만 움직일 수 있다.  
__입력 조건__  
+ 첫째 줄에 테스트 케이스의 수 T(1<=T<=10)
+ 매 테스트 케이스의 첫재 줄에는 탐사 공간의 크기를 의미하는 정수 N이 주어진다(2<=N<=125) 이어서 N개의 줄에 걸쳐 각 칸의 비용이 주어지므로 공백으로 구분한다. (0<=각 칸의 비용<=9)

__출력 조건__  
+ 각 테스트 케이스마다 0,0에서 n-1,n-1의 위치로 이동하는 최소 비용을 한 줄에 하나씩 출력한다.

```
입력 예시
3
3
5 5 4
3 9 1
3 2 7
5
3 7 2 0 1
2 8 0 9 1
1 2 1 8 1
9 8 9 2 0
3 6 5 1 5
7
9 0 5 1 1 5 3
4 1 2 1 6 5 3
0 7 6 1 6 8 5
1 1 7 8 3 2 3
9 4 0 7 6 4 1
5 8 3 2 4 8 3
7 4 8 4 8 3 4

출력 예시
20
19
36
```
### 내가 작성한 코드
```python
import heapq


def dijkstra():
    q = []
    x = y = 0
    distance[x][y] = graph[x][y]
    heapq.heappush(q, (graph[x][y], x, y))

    while q:
        cost, x, y = heapq.heappop(q)
        if distance[x][y] < cost:
            continue

        for i in range(4):
            px = x + dx[i]
            py = y + dy[i]
            if 0 <= px and px < n and 0 <= py and py < n:
                if distance[px][py] > cost + graph[px][py]:
                    distance[px][py] = cost + graph[px][py]
                    heapq.heappush(q, (distance[px][py], px, py))


t = int(input())

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]
INF = int(1e9)

for _ in range(t):

    # 탐사공간 크기
    n = int(input())

    # 방문
    distance = [[INF] * n for _ in range(n)]

    # 그래프 입력
    graph = [[] for _ in range(n)]
    for i in range(n):
        graph[i] = list(map(int, input().split()))

    dijkstra()

    print(distance[n - 1][n - 1])
```
특정위치부터 특정위치까지에 거리 최소값이므로 다이젝스트라 알고리즘으로 해결할 수 있다.


### 모범 답안
특정 위치에서 특정 위치로 이동하는 최단 거리를 계산하는 문제이므로 다익스트라 알고리즘을 사용하면 해결할 수 있다. 맵의 각 위치를 노드로 보고, 상하좌우로 모든 노드가 연결되어있다고 보면 된다. 예를 들어 위치 A와 위치 B가 서로 인접해 있다고 해보자. 이때 A -> B로 가는 비용은 B 위치의 탐사 비용이 될 것이고, B -> A로 가는 비용은 A 위치의 탐사 비용이 될 것이다.  
__n의 범위가 최대 125라 작다고 느껴서 플로이드 워셜 알고리즘을 사용하면 안 된다. 문제에서 입력 자체가 2차원 배열로 들어오기 때문에 전체 노드의 개수는 N^2으로 10,000을 넘길 수 있기 때문이다.__
```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

# 전체 테스트 케이스(Test Case)만큼 반복
for tc in range(int(input())):
    # 노드의 개수를 입력받기
    n = int(input())

    # 전체 맵 정보를 입력받기
    graph = []
    for i in range(n):
        graph.append(list(map(int, input().split())))

    # 최단 거리 테이블을 모두 무한으로 초기화
    distance = [[INF] * n for _ in range(n)]

    x, y = 0, 0 # 시작 위치는 (0, 0)
    # 시작 노드로 가기 위한 비용은 (0, 0) 위치의 값으로 설정하여, 큐에 삽입
    q = [(graph[x][y], x, y)]
    distance[x][y] = graph[x][y]

    # 다익스트라 알고리즘을 수행
    while q:
          # 가장 최단 거리가 짧은 노드에 대한 정보를 꺼내기
          dist, x, y = heapq.heappop(q)
          # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
          if distance[x][y] < dist:
              continue
          # 현재 노드와 연결된 다른 인접한 노드들을 확인
          for i in range(4):
              nx = x + dx[i]
              ny = y + dy[i]
              # 맵의 범위를 벗어나는 경우 무시
              if nx < 0 or nx >= n or ny < 0 or ny >= n:
                  continue
              cost = dist + graph[nx][ny]
              # 현재 노드를 거쳐서, 다른 노드로 이동하는 거리가 더 짧은 경우
              if cost < distance[nx][ny]:
                  distance[nx][ny] = cost
                  heapq.heappush(q, (cost, nx, ny))

    print(distance[n - 1][n - 1])
```

<br>

## 5. 숨바꼭질
---
주인공은 술래로부터 잡히지 않도록 숨을 곳을 찾고 있다. 주인공은 1 ~ N번까지의 헛간 중에서 하나를 골라 숨을 수 있으며, 술래는 항상 1번 헛간에서 출발한다. 전체 맵에는 총 M개의 양방향 통로가 존재하며, 하나의 통로는 서로 다른 두 헛간을 연결한다. 또한 전체 맵은 항상 어떤 헛간에서 다른 어떤 헛간으로 도달이 가능한 형태로 주어진다.  
주인공은 1번 헛간으로부터 최단 거리가 가장 먼 헛간이 가장 안전하다고 판단하고 있다. 이때 최단 거리의 의미는 지나야 하는 길의 최소 개수를 의미한다. 주인공이 숨을 헛간의 번호를 출력하는 프로그램을 작성하시오.  
__입력 조건__  
+ 첫째 줄에는 N과 M이 주어지며, 공백으로 구분한다. (2<=N<=20,000), (1<=M<=50,000)
+ 이후 M개의 줄에 걸쳐서 서로 연결된 두 헛간 A와 B의 번호가 공백으로 구분되어 주어진다.

__출력 조건__  
+ 첫 번째는 숨어야 하는 헛간 번호를(만약 거리가 같은 헛간이 여러 개면 가장 작은 헛간 번호를 출력한다.), 두 번째는 그 헛간까지의 거리를, 세 번째는 그 헛간과 같은 거리를 갖은 헛간의 개수를 출력한다.

```
입력 예시
6 7
3 6
4 3
3 2
1 3
1 2
2 4
5 2

출력 예시
4 2 3
```


### 내가 작성한 코드
```python
from collections import deque


def bfs():
    q = deque()
    q.append((1, 0))

    distance[1] = -1

    while q:
        idx, cost = q.popleft()
        for idx in graph[idx]:
            if distance[idx] == 0:
                distance[idx] = cost + 1
                q.append((idx, cost + 1))


n, m = map(int, input().split())
distance = [0] * (n + 1)

# 그래프 입력
graph = [[] for _ in range(n + 1)]
for _ in range(m):
    a, b = map(int, input().split())
    graph[a].append(b)
    graph[b].append(a)

bfs()

dis = max(distance)
idx = distance.index(dis)

print(idx, dis, distance.count(dis))
```
리스트의 index 함수는 해당 값의 가장 빠른 인덱스의 인덱스값을 반환한다.  
다이젝스트라로 풀 수도 있지만, 각각의 정점으로 이동거리가 1인 경우에는 bfs로도 풀 수 있다.  
이동거리가 1인경우의 bfs는 가장 먼저 방문하는 것이 가장 최단 거리의 값을 갖게 된다.

### 모범 답안
이 문제는 다익스트라 알고리즘을 이용하여 1번 노드부터 다른 모든 노드로의 최단 거리를 계산한 뒤, 가장 최단 거리가 긴 노드를 찾는 문제이다. 문제 조건에서 어느 헛간이든 도달이 가능한 형태로 주어진다고 했기 때문에 최종적인 리스트에는 INF가 없을 것이기에 추가적인 처리 없이 간단하게 해결할 수 있다.
```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드를 1번 헛간으로 설정
start = 1
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n + 1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n + 1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b = map(int, input().split())
    # a번 노드와 b번 노드의 이동 비용이 1이라는 의미(양방향)
    graph[a].append((b, 1))
    graph[b].append((a, 1))

def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정하여, 큐에 삽입
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q: # 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보를 꺼내기
        dist, now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
        if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접한 노드들을 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐서, 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

# 다익스트라 알고리즘을 수행
dijkstra(start)

# 가장 최단 거리가 먼 노드 번호(동빈이가 숨을 헛간의 번호)
max_node = 0
# 도달할 수 있는 노드 중에서, 가장 최단 거리가 먼 노드와의 최단 거리
max_distance = 0
# 가장 최단 거리가 먼 노드와의 최단 거리와 동일한 최단 거리를 가지는 노드들의 리스트
result = []

for i in range(1, n + 1):
    if max_distance < distance[i]:
        max_node = i
        max_distance = distance[i]
        result = [max_node]
    elif max_distance == distance[i]:
        result.append(i)

print(max_node, max_distance, len(result))
```



__cf) 최단경로 문제 풀면서 기억해야할 점__  
+ 항상 처음 시작 지점 처리 우선적으로 코딩할 것
+ 문제에서 특별히 0,0의 위치부터 시작하는 것이 아니라면 인덱스와 노드번호를 맞추기 위해서 n+1만큼 초기화하고 사용은 for에서 range(1,n+1)로 사용
<br>


## 주의할점
최단 경로 알고리즘 문제의 경우, 알고리즘이 정해져있다.  
+ 플로이드
+ 다이젝스트라
+ bfs(이동거리 1인 경우)
+ 벨만포드
+ 위상정렬

최단 거리 문제의 경우 위 알고리즘을 생각해보고, 만약 알고리즘을 정하고 풀이를 생각하는데 잘 풀리지 않는다면 알고리즘을 잘못 선택했을 가능성이 높다.  
만약 잘 풀이가 생각나지 않는다면 다른 알고리즘을 선택해서 생각해보자.  



<br><br><br>

---
__본 포스팅은 '이것이 코딩 테스트다 with 파이썬'을 읽고 공부한 내용을 바탕으로 작성하였습니다.__
