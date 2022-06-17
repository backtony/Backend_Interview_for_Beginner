---
layout: post
title:  DFS/BFS 기출문제
subtitle:   DFS/BFS 기출문제
categories: algorithm
tags: algorithm-intermediate
comments: true
# header-img:
---
* 
{:toc}


## 1. 간단 정리
---
+ 탐색 : 많은 양의 데이터 중에서 원하는 데이터를 찾는 과정
+ 자료구조 : 데이터를 표현하고 처리하는 방법
+ 스택 : 선입후출, 후입선출구조이며 박스 쌓기에 비유 가능
+ 큐 : 선입선출구조로 공정한 자료구조라고도 한다. 대기 줄에 비유 가능
+ DFS : Depth-First Search, 깊이 우선 탐색 알고리즘이며 그래프를 탐색하는 알고리즘이다. 최대한 멀리 있는 노드를 우선으로 탐색하는 방식으로 동작하며 스택자료구조를 이용
+ BFS : 너비우선 탐색으로 가까운 노드부터 탐색하는 알고리즘이다. 큐를 이용하면 효과적으로 구현 가능

<br>

## 2. 특정한 거리의 도시 찾기
---
[문제 클릭](https://www.acmicpc.net/problem/18352){: target="_blank"}

### 내가 작성한 코드
```python
import sys
import heapq
input = sys.stdin.readline

# 도시의 개수, 도로의 개수, 거리 정보, 출발 도시 번호
n, m, k, x = map(int, input().split())
INF = int(1e9) # 무한

shortcut = [INF]*(n+1) # 각 도시의 최단 경로
graph =[[] for _ in range(n+1)] # 도시별 연결 정보
q=[] # 우선순위 큐

# 도로 정보 입력
for _ in range(m):
    a,b = map(int,input().split())
    graph[a].append(b)

# 출발지점 정보 수정 및 우선순위 큐
shortcut[x] = 0
heapq.heappush(q,(0,x))

# 최소 거리 구하기
while q:
    distance, now = heapq.heappop(q)
    # 이미 처리된 경우는 무시 , 첫 시작의 경우가 등호에 해당하므로 등호는 뺀다
    if distance > shortcut[now]:
        continue
    for way in graph[now]: # now에 연결된 도시들
            # 갱신이 필요한 경우
            if distance + 1 < shortcut[way]:
                shortcut[way] = distance+1
                heapq.heappush(q,(shortcut[way],way))

cnt=0
for i in range(1,n+1):
    if shortcut[i] == k:
        print(i)
        cnt+=1
if cnt == 0:
    print(-1)
```
한 가지 출발지점이 정해진 경우에 대해서 각 지점에 대해 최소 거리를 구하는 다익스트라 알고리즘을 사용했다. 다익스트라 알고리즘의 복잡도는 선형로그시간 O(ElogV)이므로 주어진 큰 범위에 적합한 알고리즘이다. (V는 노드, E는 간선, 우선순위 큐로 인해 logV)
<br>

2차 리뷰 코드
```python
import sys
from collections import deque

input = sys.stdin.readline

def bfs(start):
    q = deque()
    distance[start] = 0  # 시작지점 방문처리
    q.append(start)

    while q:
        next = q.popleft()
        for destination in graph[next]:
            # 가중치가 1인 경우에는 먼저 들어오는 것이 가장 최소값으로 
            # 거리가 갱신되지 않았을 때만 거리를 갱신하면 된다.
            if distance[destination] == -1:
                distance[destination] = distance[next] + 1
                q.append(destination)

# 조건 입력
n, m, k, x = map(int, input().split())

# 최단거리
distance = [-1] * (n + 1)

# 그래프 입력
graph = [[] for _ in range(n + 1)]
for i in range(m):
    a, b = map(int, input().split())
    graph[a].append(b)

bfs(x)

key = 1
for i in range(1, n + 1):
    if distance[i] == k:
        key = 0
        print(i)

if key:
    print(-1)
```
답안과 같이 bfs로 풀었는데 한 번 시간초과가 떴다. 확인해보니 큐를 안쓰고 그냥 리스트의 pop(0)을 사용한 것이 문제였다. pop(0)도 당연히 복잡도가 O(1)일 것이라 생각했는데 pop은 맨 뒤에 것을 뽑아주기때문에 pop(0)을 하면 맨 앞으로까지 와서 빼주는 것이라 O(N)의 복잡도를 가진다는 것을 처음 알았다. 큐를 사용하면 O(1)의 복잡도가 소요된다.

### 모범 답안
그래프에서 __간선비용이 모두 동일할 때는 BFS__ 를 이용하여 최단 거리를 찾을 수 있다.  
문제 조건에서 노드의 개수 N은 최대 300,000개이며 간선의 개수 M은 최대 1,000,000개이다. 따라서 BFS를 이용해 O(N+M)으로 동작하는 소스 코드를 작성하여 시간 초과 없이 해결할 수 있다.(선형 시간 알고리즘에서는 천만까지 범위가 가능하다.) 먼저 특정한 도시 X를 시작점으로 BFS를 수행하여 모든 도시까지의 최단 거리를 계산한 뒤, 각 최단 거리를 하나씩 확인하며 그 값이 K인 경우에 해당 도시의 번호를 출력하면 된다.  
간선 정보에서 각각의 거리가 다르다면 다익스트라를 써야하지만, __비용이 모두 같다면 시작지점으로부터 연결되있는 차례대로 비용을 계산하면 그 자체가 최소거리가 되기 때문에__ BFS를 사용해도 된다.  
다익스트라의 경우는 간선비용이 다를 때 같을 때 모두 사용할 수 있다. 그래서 나는 다익스트라를 알아두는게 좋을 것 같다는 생각이 든다. BFS와 코드도 매우 비슷하다. 단지 큐 대신 우선순위 큐를 사용한다는 점 이외에는 BFS와 비슷하다.
```python
import sys
from collections import deque

n, m, k, x = map(int, input().rstrip().split())

graph = [[] for _ in range(n + 1)]
distance = [-1] * (n + 1)  # 최단 거리
distance[x] = 0  # 시작위치 0
# 간선 정보 입력
for i in range(m):
    a, b = map(int, input().rstrip().split())
    graph[a].append(b)

q = deque([x])
while q:
    now = q.popleft()
    # 현재 위치에서 연결되어있는 노드
    for way in graph[now]:
        # 최단 거리 갱신이 안되어있다면
        if distance[way] == -1:
            # 최단거리 갱신
            distance[way] = distance[now] + 1
            # 큐 삽입
            q.append(way)

cnt = False  # k있는지 판단할 변수
for i in range(1, n + 1):
    if distance[i] == k:
        cnt = True
        print(i)
if cnt == False:
    print(-1)
```

## 3. 연구소
---
[문제 클릭](https://www.acmicpc.net/problem/14502){: target="_blank"}  

### 내가 작성한 코드
모범답안 코드는 python3로 제출시 시간초과가 뜨는데 내 코드는 python3로 해도 시간초과가 뜨지 않는다. 그래도 답안 코드도 배울점이 있다.   
import sys를 이용할 경우에도 시간초과가 뜨는데 엄청나게 입력이 많은 경우가 아니면 sys를 안쓰는게 좋은 것 같다.   
__설계 과정__  
범위가 매우 적으니 모든 경우를 고려해도 될 것이라고 생각했다. 그러면 그래프를 입력받고 칸막이를 세웠다가 지웠다가를 반복해야 하므로 또 다른 그래프를 복사해서 사용하는게 좋을 것 같다고 생각했다. itertools의 combinations를 이용해서 칸막이를 세울 칸을 정했고, dfs를 이용해서 바이러스 전파를 진행했다.
```python
from itertools import combinations
import copy

# 벽 세우기
def makeBlock(positions):
    for x,y in positions:
        tmpGraph[x][y] = 1


# 바이러스 전파
def dfs(x, y):
    tmpGraph[x][y] = 2
    for i in range(4):
        px = x + dx[i]
        py = y + dy[i]
        if 0 <= px and px < n and 0 <= py and py < m:
            if tmpGraph[px][py] == 0:
                dfs(px, py)


n, m = map(int, input().split())

graph = []
blank = []
virus = []
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]
answer = 0

# 그래프 입력
for i in range(n):
    tmp = list(map(int, input().split()))
    graph.append(tmp)
    # 빈칸 좌표, 바이러스 추출
    for j in range(m):
        if tmp[j] == 0:
            blank.append([i, j])
        elif tmp[j] == 2:
            virus.append([i, j])

# 벽돌 좌표 추출
for positions in list(combinations(blank, 3)):
    tot = 0
    tmpGraph = copy.deepcopy(graph)
    makeBlock(positions)
    # 바이러스 전파
    for x, y in virus:
        dfs(x, y)
    # 0 개수 세기
    for i in range(n):
        tot += tmpGraph[i].count(0)
    answer = max(answer, tot)

print(answer)

```
__모범 답안의 재귀함수로 구현한 부분은 사실 조합이 아니다. 생각해보면 2중 for문을 한바퀴 돌고 2번째 칸막이를 다시 선택한 뒤에 3번째 칸막이를 선택하는 과정에서 중복이 발생한다. 따라서 완벽한 조합을 구하는 과정은 아니다.__

### 모범 답안
이 문제는 벽을 3개 설치하는 모든 경우의 수를 다 계산해야 한다. 간단하게 생각해보면 전체 맵의 크기가 8 * 8 이므로, 벽을 설치할 수 있는 모든 조합의 수는 최악의 경우 (바이러스가 하나도 존재하지 않는 경우) 64C3이 될 것이다. 이는 100,000보다도 작은 수이므로, 대략 선형 로그 시간의 알고리즘을 설계하면 되는데 주요 풀이 알고리즘이 BFS/DFS 이므로 인접 리스트를 사용하면 선형 시간 알고리즘으로 풀이할 수 있다. 따라서 모든 경우의 수를 고려해도 제한 시간 안에 문제를 해결할 수 있다는 것을 알 수 있다.  
또한 모든 조합을 계산할 때는 파이썬의 조합 라이브러리를 사용하거나, DFS 혹은 BFS를 이용하여 해결할 수 있다. 따라서 벽의 개수가 3개가 되는 모든 조합을 찾은 뒤에 그러한 조합에 대해서 안전 영역의 크기를 계산하면 된다. 안전영역의 크기를 구하는 것 또한 DFS나 BFS를 이용하여 계산할 수 있다. 결과적으로 여기서는 가능한 모든 경우의 수를 계산하되, 안전 영역을 계산할 때 DFS나 BFS를 적절히 사용해야 된다는 것이다.  
문제 풀이 아이디어를 간략히 설명함현, 초기에 비어 있는 모든 공간 중에서 3개를 골라 벽을 설치하는 것이다. 매번 벽을 설치할 때마다, 각 바이러스가 사방으로 퍼지는 것을 BFS/DFS로 계산하여 안전 영역을 구해야 한다.  
python3 로 제출시 시간초과가 발생하고 pypy3로 하면 합격점을 받을 수 있다.
```python

n, m = map(int, input().split())

# 주어진 그래프와 벽 세우고 난 후의 그래프
graph = []
temp = [[0] * m for _ in range(n)]
result = 0  # 안전 영역 개수
# 시계방향
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

# 그래프 입력
for _ in range(n):
    graph.append(list(map(int, input().split())))


# dfs형식을 통한 바이러스 전염
def virus(x, y):
    for i in range(4):
        px = x + dx[i]
        py = y + dy[i]
        # 범위 내, 빈칸
        # 조건을 0<= px <n 으로 합치는 것보다 각각 쓰는게 더 빠르게 걸러진다.
        if 0 <= px and px < n and 0 <= py and py < m and temp[px][py] == 0:
            temp[px][py] = 2
            virus(px, py)  # 재귀적 dfs


# 안전 영역 카운트
def score():
    cnt = 0
    for i in range(n):
        for j in range(m):
            if temp[i][j] == 0:
                cnt += 1
    return cnt


# 모든 경우의 칸 세우기
def dfs(count):
    global result
    # 벽이 모두 설치되었을 때
    if count == 3:
        # 그래프 옮기기
        for i in range(n):
            for j in range(m):
                temp[i][j] = graph[i][j]
        # 바이러스 전파
        for i in range(n):
            for j in range(m):
                if temp[i][j] == 2:
                    virus(i, j)
        result = max(result, score())
        return

    # 울타리 세우기
    for i in range(n):
        for j in range(m):
            # 빈칸이면
            if graph[i][j] == 0:
                graph[i][j] = 1  # 벽설치
                count += 1
                dfs(count)
                count -= 1
                graph[i][j] = 0  # 벽설치 해제


dfs(0)
print(result)
```
__배운 점__  
처음 설계할 때 for문으로 울타리를 세우면 되겠다고는 생각했지만 해결이되지 않아 itertools를 사용했었다. 하지만 답안에서는 재귀적 사고를 통해 for문으로 울타리를 세웠다. 저런 방식도 기억해두는게 좋을 것 같다.

<br>

## 4. 경쟁적 전염
---
[문제 클릭](https://www.acmicpc.net/problem/18405){: target="_blank"}  

### 내가 작성한 코드
```python
def solution():
    cnt = 0
    # 현재 virus에 들어있는 길이만큼을 미리 저장하고
    # 그 만큼만 돌리고 cnt해주고 다시 길이를 구하는 식으로 반복
    while cnt != s:
        length = len(virus)
        # while로 virus꺼내면 virus에 계속 추가되서 카운트를 할 수 없으므로 for문사용
        for _ in range(length):
            num, x, y = virus.pop(0)
            for i in range(4):
                px = x + dx[i]
                py = y + dy[i]
                # 범위내고 비어있다면 전염시키고 해당 위치 삽입
                if 0 <= px and px < n and 0 <= py and py < n and graph[px][py] == 0:
                    graph[px][py] = num
                    virus.append((num, px, py))
        cnt += 1


# N시험관크기, K바이러스 종류개수
n, k = map(int, input().split())

graph = []
virus = []

# 시계방향
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

# 맵 입력
for _ in range(n):
    graph.append(list(map(int, input().split())))

# 바이러스 위치 저장
for i in range(n):
    for j in range(n):
        if graph[i][j] != 0:
            # 바이러스 번호, 위치
            virus.append((graph[i][j], i, j))

virus.sort()  # 바이러스 번호순 정렬

# s초후, x,y위치
s, x, y = map(int, input().split())
solution()
print(graph[x - 1][y - 1])
```
정렬을 해야하는데 deque에는 sort기능이 없어서 그냥 리스트를 사용했고 pop(인덱스)로 꺼냈다.  
<br>

2차 리뷰 코드  
우선순위 큐를 이용해서 코딩했다. 시간,넘버,위치,저장 순으로 저장하면 순서대로 오름차순으로 정렬되어 뽑아지므로 따로 작업할 필요가 없이 시간만 고려하면 되기에 좀 더 짧게 코딩할 수 있었다. 지금 보니 1차 코드는 좋지 못한 코드인 것 같고 2차 코드나 답안이 좋은 코드인 것 같다.(pop을 쓴것도 그렇고)
```python
import heapq

n, k = map(int, input().split())
graph = []
q = []
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]
# 그래프 정보
for i in range(n):
    graph.append(list(map(int, input().split())))
    for j in range(n):
        # 바이러스가 있으면 시간,넘버, 위치 저장
        if graph[i][j] != 0:
            heapq.heappush(q,(0,graph[i][j], i, j))

s, x, y = map(int, input().split())

while q:
    cnt,num,a,b = heapq.heappop(q)
    if cnt == s:
        break
    for i in range(4):
        pa = a + dx[i]
        pb = b + dy[i]
        if 0<=pa and pa<n and 0<=pb and pb<n and graph[pa][pb]==0:
            graph[pa][pb]=num
            heapq.heappush(q, (cnt + 1, num, pa, pb))

print(graph[x-1][y-1])
```

### 모범 답안
낮은 번호부터 증식하므로, 초기에 큐에 원소를 삽입할 때는 낮은 바이러스의 번호부터 삽입해야 한다. 이후 BFS를 수행하며 방문하지 않은 위치를 차례대로 방문하도록 하면 된다.
```python
from collections import deque

n, k = map(int, input().split())

graph = [] # 전체 보드 정보를 담는 리스트
data = [] # 바이러스에 대한 정보를 담는 리스트

for i in range(n):
    # 보드 정보를 한 줄 단위로 입력
    graph.append(list(map(int, input().split())))
    for j in range(n):
        # 해당 위치에 바이러스가 존재하는 경우
        if graph[i][j] != 0:
            # (바이러스 종류, 시간, 위치 X, 위치 Y) 삽입
            data.append((graph[i][j], 0, i, j))

# 정렬 이후에 큐로 옮기기 (낮은 번호의 바이러스가 먼저 증식하므로)
data.sort()
q = deque(data)
 
target_s, target_x, target_y = map(int, input().split())
 
# 바이러스가 퍼져나갈 수 있는 4가지의 위치
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

# 너비 우선 탐색(BFS) 진행
while q:
    virus, s, x, y = q.popleft()
    # 정확히 s초가 지나거나, 큐가 빌 때까지 반복
    if s == target_s:
        break
    # 현재 노드에서 주변 4가지 위치를 각각 확인
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        # 해당 위치로 이동할 수 있는 경우
        if 0 <= nx and nx < n and 0 <= ny and ny < n:
            # 아직 방문하지 않은 위치라면, 그 위치에 바이러스 넣기
            if graph[nx][ny] == 0:
                graph[nx][ny] = virus
                q.append((virus, s + 1, nx, ny))

print(graph[target_x - 1][target_y - 1])
```
__배울 점__  
+ 내가 작성한 코드는 for문으로 정보를 입력 받고 다시 for문을 돌려 바이러스의 위치를 찾았는데 답안 코드에서는 입력과 동시에 바로 아래 for문을 이용해서 바이러스의 위치를 찾았다. 코드를 좀 더 줄일 수 있는 좋은 방법인 것 같다.
+ deque에는 sort가 없어서 그냥 리스트를 이용했는데 답안은 리스트로 받아서 sort한 뒤에 deque(정렬한리스트)를 넣어서 사용했다. deque의 활용법을 좀 더 기억해야겠다.
+ 큐에 넣을 때 시간의 정보를 추가로 넣어줬다면 for문을 줄일 수 있었다.

<br>

## 5. 괄호 변환
---
[문제 클릭](https://programmers.co.kr/learn/courses/30/lessons/60058){: target="_blank"}  

### 내가 작성한 코드
재귀부분에서 약간의 생각이 필요했지만 문제에서 거의 모든 내용이 주어졌기때문에 그대로 따라가면 쉽게 해결할 수 있다.
```python
def check(u):
    left = 0
    right = 0
    for i in range(len(u)):
        if u[i] == '(':
            left += 1
        else:
            right += 1
        # ) 가 더 많게되면 올바르지 않음
        if left < right:
            return False
    return True


def solution(p):
    length = len(p)
    # 빈문자열 반환
    if length == 0:
        return p

    u = ""
    left = 0
    right = 0
    idx = 0
    # 균형 문자열 뽑아내기
    while (idx < length):
        if p[idx] == '(':
            left += 1
        else:
            right += 1
        u += p[idx]
        idx += 1

        # 균현 잡힘
        if left == right:
            v = p[idx:]
            # 올바르면 나머지에 대한 작업 반복
            if check(u):
                return u + solution(v)

            # 올바르지 않으면
            else:
                tmp = "(" + solution(v) + ")"
                u = u[1:-1]
                for i in range(len(u)):
                    if u[i] == "(":
                        tmp += ")"
                    else:
                        tmp += "("
                return tmp
```
문자열 String의 경우 리스트 처럼 u[i] = ")" 이런식으로 교체가 불가능하다. 따라서 + 연산을 사용해야했다.


### 모범  답안
구현을 위한 알고리즘 자체는 문제에 그대로 제시되어 있기 때문에, 재귀 함수를 이용하여 문제에 기재되어 있는 알고리즘을 안정적으로 구현할 수 있으면 해결할 수 있다.  
실수 없이 풀려면 소스코드를 최대한 단순화하는 것이 좋다. 따라서 특정 문자열에서 '균형잡힌 괄호 문자열'의 인덱스를 반환하는 함수와 특정한 '균형잡힌 괄호 문자열'이 '올바른 괄호 문자열'인지 판단하는 함수를 별도로 구현하고 재귀 함수에서 이 두 함수를 불러오도록 소스코드를 작성하자.  

```python
# 균형잡힌 문자열 분리
def balance(p):
    count = 0
    for i in range(len(p)):
        if p[i] == '(':
            count += 1
        else:
            count -= 1
        # 균형 잡힌 순간의 인덱스 반환
        # 입력 자체가 균형잡힌 괄호 문자열로 주어지므로 결국 return 발생
        if count == 0:
            return i


# 올바른 괄호 문자열 판단
def proper(u):
    count = 0
    for i in range(len(u)):
        if u[i] == '(':
            count += 1
        else:
            # count==0인 시점에 )가 오면 올바른 문자열이 아님
            if count == 0:
                return False
            count -= 1
    return True


# 균형잡힌 괄호 문자열을 올바른 괄호 문자열로 반환하는 솔루션
def solution(p):
    answer = ''
    # 빈 문자열일 경우 빈 문자열 반환
    if p == '':
        return p
    idx = balance(p)
    u = p[:idx + 1]
    v = p[idx+1:]
    # 올바른 문자열이라면
    if proper(u):
        answer = u + solution(v)
    # 올바른 문자열이 아니라면
    else:
        answer = '('
        answer += solution(v)
        answer += ')'
        # 앞 뒤 문자 제거
        u = list(u[1:-1]) # 문자열로 표현되기때문에 list로 형변환
        # 뒤집기
        for i in range(len(u)):
            if u[i] == '(':
                u[i] = ')'
            else:
                u[i] = '('
        answer += ''.join(u) # 리스트를 다시 문자열로
    return answer
```
<br>

## 6. 연산자 끼워 넣기
---
[문제 클릭](https://www.acmicpc.net/problem/14888){: target="_blank"}  

### 내가 작성한 코드
연산자 갯수가 n-1개 이므로 n-1!하면 모든 경우의수가 나온다. 3백만 정도의 연산 횟수가 되므로 완전 탐색을 해도 될 것 같아서 다음과 같이 설계했다. permutation의 복잡도는 O(n!) 
```python
# 최소 최대값을 구해야하므로 연산 다 해봐야함
# 연산자 순서가 상관있으므로 permutations

from itertools import permutations

n = int(input())
num = list(map(int, input().split()))
table = list(map(int, input().split()))
units = ['+'] * table[0] + ['-'] * table[1] + ['*'] * table[2] + ['/'] * table[3]



# set에 관해서
# data ={1,2,3,4,5,1,1,1} 자동 중복 제거
# data = {(1,1),(1,1),(2,1),(1,2)} # 완전 같은 1,1은 제거 순서 다른 것은 제거 안됨

def solution():
    min_ans = int(1e9)
    max_ans = -int(1e9)


    # {(),(),()} 형식으로 되있고 () 하나씩 뽑아온다.
    # set으로 중복 제거
    for unit in set(permutations(units,n-1)):
        tmp = num[0]
        for i in range(n - 1):
            if unit[i] == '+':
                tmp += num[i + 1]
            elif unit[i] == '-':
                tmp -= num[i + 1]
            elif unit[i] == '*':
                tmp *= num[i + 1]
            else:
                tmp= int(tmp/num[i+1])
        max_ans = max(max_ans, tmp)
        min_ans = min(min_ans, tmp)
    return max_ans, min_ans


max_ans, min_ans = solution()

print(max_ans)
print(min_ans)
```
파이썬은 느리므로 최적화가 필수이고 itertools를 사용할 때는 항상 복잡도에 대해 생각해야 한다.  
이 문제에서는 어느정도의 중복을 set을 사용하여 완화시킬 수 있다.  
set으로 중복을 제거하지 않고 permutations 그대로 사용하면 중복이 생긴다. 예를 들면, * * + 가 있다고 하면 permutations에서  *는 서로 다른 것으로 취급되어 * * +가 두 번 나오게 된다.  
또한, len()을 이용해 for문을 돌리면 반복적으로 len을 계산하는 경우가 생기므로 밖으로 빼서 계산하고 그걸 사용하도록 한다.  
파이썬의 경우 음수 몫의 나눗셈의 경우 올림을 한다.(-1//2 의 경우 -0.5이므로 -1이 나오게 된다.)  
하지만 문제에서는 내림을 하라고 요구되고 있으므로 그냥 나눗셈을 한 뒤, int로 형변환을 해서 나머지를 버리면 된다.  


### 모범 답안
최대 11개의 수가 주어졌을 때, 각 수와 수 사이에 사칙연산 중 하나를 삽입하는 모든 경우에 대하여 만들어질 수 있는 결과의 최댓값 및 최솟값을 구하면 된다. 따라서 모든 경우의 수를 계산하기 위하여 완전탐색(DFS / BFS)를 이용하여 해결할 수 있다.  
이 문제에서는 각 사칙연산을 중복하여 사용할 수 있기 때문에, 중복 순열을 이용해 풀 수도 있다. 하지만 DFS를 이용하여 풀 수도 있다.  
__여기서 기억해야 할 점은 중복 순열을 DFS로 나타낼 수 있다는 것이다.__  
```python
n = int(input())
num = list(map(int, input().split()))
plus, minus, time, divide = map(int, input().split())

min_ans = int(1e9)
max_ans = -int(1e9)

# 백트래킹 -> 해를 찾는 도중에 막히면 되돌아가서 다시 해를 찾는 기법 -> 재귀를 이용한 완전 검색
def solution(cnt, tot):
    global plus, minus, time, divide, min_ans, max_ans

    # n번째 인덱스까지 도달시 max, min 수정하고 다른 경우로 돌아가기
    if cnt == n:
        max_ans = max(max_ans, tot)
        min_ans = min(min_ans, tot)
        return
    
    # 재귀적 사고
    if plus > 0:
        plus -= 1
        solution(cnt + 1, tot + num[cnt])
        plus += 1

    if minus > 0:
        minus -= 1
        solution(cnt + 1, tot - num[cnt])
        minus += 1

    if time > 0:
        time -= 1
        solution(cnt + 1, tot * num[cnt])
        time += 1

    if divide > 0:
        divide -= 1
        solution(cnt + 1, int(tot / num[cnt]))
        divide += 1


solution(1, num[0])
print(max_ans)
print(min_ans)
```
__위와 같이 코딩하면 마지막에는 빼줬던 것을 전부다 회수하면서 if문이 끝나 solution 함수가 끝나게 된다.__  
c++의 나눗셈 몫은 파이썬에서 나눗셈에 int를 씌운것과 같다. 재귀로 코딩할 때 elif가 아닌 if를 사용하는 이유는 elif 사용시 남아있어도 선택이 안되고 넘어가기 때문에 전부 선택하기 위해서는 if를 사용해서 모두 선택해줘야 한다.

__python 음수 나눗셈__  
[![그림1](https://backtony.github.io/assets/img/post/python/intermediate/intermediate-3.PNG)](https://kj-said.tistory.com/entry/Python-%EB%82%98%EB%88%97%EC%85%88%EC%97%90-%EA%B4%80%ED%95%9C-%EA%B3%A0%EC%B0%B0-%EC%9D%8C%EC%88%98-%EB%82%98%EB%88%84%EA%B8%B0-divmod){: target="_blank"}  

그림과 같이 몫은 좌측값, 즉, 작은 값을 가리킨다. 따라서 연산 결과 아래와 같다.
```python
2018 / 5 # 403.6
2018 // 5 # 403

-2018 / 5 # -403.6
-2018 // 5 # -404 
```
즉, 파이썬의 경우 음수 몫의 나눗셈의 경우 올림을 한다.  
하지만 문제에서는 내림을 하라고 요구되고 있으므로 그냥 나눗셈을 한 뒤, int로 형변환을 해서 나머지를 버리면 된다.

<br>


#### DFS 중간정리
3번, 6번을 못 풀었었는데 모두 DFS문제였다. 
```python  
count += 1
dfs(count)
count -= 1
```
dfs는 위와 같은 형태로 대부분 인자를 탈출조건에 사용했으며, 간단히 정리하자면 아래와 같다.  
+ 만약 3개를 선택했다고 가정하면, 먼저 선택한 2개는 유지하면서 나중에 선택한 1개를 다른 것으로 바꾸기.. 이후에 남은 것들을 다 선택했다면 2번째 선택했던 것을 바꾸고 마지막 선택한 것을 다시 처음부터 바꾸기 이 과정을 반복하는데 사용되었다.
+ 특정한 개수를 모두 선택한 뒤 서로의 순서를 바꾸는, 즉, 중복순열을 나타낼 때도 사용할 수 있었다. 재귀를 통해 구현되기 때문에 __최종 결과값을 저장할 변수는 global 키워드가 필요하다.__    
+ __중복순열, 순열에서 DFS를 사용할 수 있다는 것을 기억하자__

## 7. 감시 피하기
---
[문제 클릭](https://www.acmicpc.net/problem/18428){: target="_blank"}  

### 내가 작성한 코드
전체 칸이 최대 36칸이고 이 중에서 3개를 골라 벽을 설치하는 경우 36C3, 총 경우의 수도 매우 적고 DFS를 사용할 것이므로 시간 초과없이 풀이 가능하다고 생각해서 모든 경우의 수를 생각했다. 위에서 다른 문제를 풀어보았을 때 itertools를 사용할 때와 dfs를 사용해서 재귀적으로 풀었을 때 서로 다른 시간차이를 보여서 이 문제도 combinations로 선택한 풀이와 dfs 재귀로 선택한 풀이 두 개로 풀어 보았다. 결과적으로 둘 다 정답처리 되었는데 생각해보면 위에서 itertools를 사용해서 시간초과 받은 문제는 permutations였다. __경험적으로 보았을 때 조합의 경우 재귀와 combinations의 차이가 크지 않으니 combinations을 우선적으로 사용하고 시간초과가 난다면 재귀를 사용하는게 좋은 것 같고, 순열의 경우 permutation과 재귀의 시간 차이가 크니 재귀적 풀이를 우선적으로 사용하는게 좋을 것 같다.__   
__combinations 풀이__
```python
from itertools import combinations
import copy

n = int(input())

graph = []
tc = []
empty = []

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]


def check(graph, spots):
    tmp = copy.deepcopy(graph)
    # 장애물
    for spot in spots:
        x, y = spot
        tmp[x][y] = 'O'
    # 선생님 위치에서 4방향 확인
    for spot in tc:
        # 숨기 실패
        if not dfs(tmp, spot):
            return False
    # 모든 선생님의 위치에서 검사 후 False리턴 없으면 숨기 성공
    return True


def dfs(graph, spot):
    x, y = spot
    for i in range(4):
        px = x + dx[i]
        py = y + dy[i]
        # 범위 내에서 반복
        while 0 <= px and px < n and 0 <= py and py < n:
            # 숨기 실패
            if graph[px][py] == 'S':
                return False
            # 현재 방향에 대해서는 숨기 성공
            elif graph[px][py] == 'O':
                break
            else:
                px += dx[i]
                py += dy[i]
    # 걸림이 없었다면 숨기 성공
    return True


# 그래프 입력받고 학생, 선생님, 빈칸 위치 저장
for i in range(n):
    graph.append(input().split())
    for j in range(n):
        if graph[i][j] == 'T':
            tc.append((i, j))
        elif graph[i][j] == 'X':
            empty.append((i, j))

key = 0
for spots in combinations(empty, 3):
    # 숨기 성공시 key값 수정
    if check(graph, spots):
        key = 1
        break

if key:
    print('YES')
else:
    print('NO')
```
__dfs 재귀 풀이__  
```python
n = int(input())

graph = []
tc = []
empty = []

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]


def check(graph):
    # 선생님 위치에서 4방향 확인
    for spot in tc:
        # 숨기 실패
        if not dfs(graph, spot):
            return False
    # 모든 선생님의 위치에서 검사 후 False리턴 없으면 숨기 성공
    return True


def dfs(graph, spot):
    x, y = spot
    for i in range(4):
        px = x + dx[i]
        py = y + dy[i]
        # 범위 내에서 반복
        while 0 <= px and px < n and 0 <= py and py < n:
            # 숨기 실패
            if graph[px][py] == 'S':
                return False
            # 현재 방향에 대해서는 숨기 성공
            elif graph[px][py] == 'O':
                break
            else:
                px += dx[i]
                py += dy[i]
    # 걸림이 없었다면 숨기 성공
    return True


# 그래프 입력받고 학생, 선생님, 빈칸 위치 저장
for i in range(n):
    graph.append(input().split())
    for j in range(n):
        if graph[i][j] == 'T':
            tc.append((i, j))
        elif graph[i][j] == 'X':
            empty.append((i, j))
ans=0
def solution(cnt):
    global ans
    if cnt == 3:
        # 숨기 성공
        if check(graph):
            ans=1
            return True
        # 숨기 실패
        else:
            return False

    # 장애물 설정
    for i in range(n):
        for j in range(n):
            if graph[i][j] == 'X':
                graph[i][j]='O'
                if solution(cnt+1):
                    return True
                graph[i][j] = 'X'
    return False

solution(0)
if ans:
    print('YES')
else:
    print('NO')
```


### 모범 답안
장애물을 3개 설치하는 모든 경우의 수는 얼마나 될지 생각해보자. 복도의 크기는 N * N이며, N은 최대 6이다. 따라서 모든 조합의 수는 최악의 경우 36C3이 된다. 이는 10,000이하의 수이므로 모든 조합을 고려하여 완전 탐색을 수행해도 시간 초과 없이 해결할 수 있다. 따라서 모든 조합을 찾기 위해서 DFS 혹은 BFS를 이용해 모든 조합을 반환하는 함수를 작성하거나, 파이썬의 조합 라이브러리를 사용할 수 있다. 여기서는 파이썬의 조합 라이브러리를 사용하겠다.  
내가 푼 풀이보다 코드는 길지만 해석해보면 시간은 훨씬 모범 답안이 빠르다고 확신할 수 있다.
```python
from itertools import combinations

n = int(input()) # 복도의 크기
board = [] # 복도 정보 (N x N)
teachers = [] # 모든 선생님 위치 정보
spaces = [] # 모든 빈 공간 위치 정보

for i in range(n):
    board.append(list(input().split()))
    for j in range(n):
        # 선생님이 존재하는 위치 저장
        if board[i][j] == 'T':
            teachers.append((i, j))
        # 장애물을 설치할 수 있는 (빈 공간) 위치 저장
        if board[i][j] == 'X':
            spaces.append((i, j))

# 특정 방향으로 감시를 진행 (학생 발견: True, 학생 미발견: False)
def watch(x, y, direction):
    # 왼쪽 방향으로 감시
    if direction == 0:
        while y >= 0:
            if board[x][y] == 'S': # 학생이 있는 경우
                return True
            if board[x][y] == 'O': # 장애물이 있는 경우
                return False
            y -= 1
    # 오른쪽 방향으로 감시
    if direction == 1:
        while y < n:
            if board[x][y] == 'S': # 학생이 있는 경우
                return True
            if board[x][y] == 'O': # 장애물이 있는 경우
                return False
            y += 1
    # 위쪽 방향으로 감시
    if direction == 2:
        while x >= 0:
            if board[x][y] == 'S': # 학생이 있는 경우
                return True
            if board[x][y] == 'O': # 장애물이 있는 경우
                return False
            x -= 1
    # 아래쪽 방향으로 감시
    if direction == 3:
        while x < n:
            if board[x][y] == 'S': # 학생이 있는 경우
                return True
            if board[x][y] == 'O': # 장애물이 있는 경우
                return False
            x += 1
    return False

# 장애물 설치 이후에, 한 명이라도 학생이 감지되는지 검사
def process():
    # 모든 선생의 위치를 하나씩 확인
    for x, y in teachers:
        # 4가지 방향으로 학생을 감지할 수 있는지 확인
        for i in range(4):
            if watch(x, y, i):
                return True
    return False

find = False # 학생이 한 명도 감지되지 않도록 설치할 수 있는지의 여부

# 빈 공간에서 3개를 뽑는 모든 조합을 확인
for data in combinations(spaces, 3):
    # 장애물들을 설치해보기
    for x, y in data:
        board[x][y] = 'O'
    # 학생이 한 명도 감지되지 않는 경우
    if not process():
        # 원하는 경우를 발견한 것임
        find = True
        break
    # 설치된 장애물을 다시 없애기
    for x, y in data:
        board[x][y] = 'X'

if find:
    print('YES')
else:
    print('NO')
```

## 8. 인구 이동
---
[문제 클릭](https://www.acmicpc.net/problem/16234){: target="_blank"}  

### 내가 작성한 코드
답안 코드와 내가 작성한 코드 모두 python3로 제출 시 시간초과가 나온다.
```python
from collections import deque

# 나라수, l명이상 r명 이하
n, l, r = map(int, input().split())
country=[]

# 나라 정보 입력
for _ in range(n):
    country.append(list(map(int, input().split())))

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

def bfs(graph, x, y):
    q = deque()
    q.append((x,y))
    tot = graph[x][y]  # 연합 총 인구수
    visit[x][y] = 1
    spots = [(x, y)]  # 연합 나라 위치
    while q:
        x, y = q.popleft()
        for i in range(4):
            px = x + dx[i]
            py = y + dy[i]
            # 범위 내, 방문하지 않은 경우
            if 0 <= px and px < n and 0 <= py and py < n and visit[px][py]==0:
                # 차이가 l이상 r이하
                if l <= abs(graph[x][y] - graph[px][py]) <= r:
                    # tot 수정, 좌표 삽입, visit 처리, q에 대입
                    tot += graph[px][py]
                    spots.append((px, py))
                    visit[px][py] = 1
                    q.append((px,py))

    # tot 정보 수정
    tot = int(tot // len(spots))

    for spot in spots:
        x, y = spot
        graph[x][y] = tot

    # 변경 값이 없으면
    if len(spots) == 1:
        return 0
    # 변경값이 있으면
    return 1


cnt = 0
while 1:
    ans = 0
    visit = [[0] * n for _ in range(n)]  # 방문 표시
    for i in range(n):
        for j in range(n):
            if visit[i][j] == 0:
                ans = max(ans, bfs(country, i, j))
    # 변경값이 있으면 카운트
    if ans:
        cnt += 1
    else:
        break

print(cnt)
```

### 모범 답안
모든 나라의 위치에서 DFS 혹은 BFS를 수행하여 인접한 나라의 인구수를 확인한 뒤에, 가능하다면 국경선을 열고 인구 이동 처리를 진행하면 된다.  
모범 답안과 내 풀이 코드를 비교했을 때 내 코드가 처리시간이 더 빨랐지만 거의 차이는 없었다. 
```python
from collections import deque

# 땅의 크기(N), L, R 값을 입력받기
n, l, r = map(int, input().split())

# 전체 나라의 정보(N x N)를 입력 받기
graph = []
for _ in range(n):
    graph.append(list(map(int, input().split())))

dx = [-1, 0, 1, 0]
dy = [0, -1, 0, 1]

# 특정 위치에서 출발하여 모든 연합을 체크한 뒤에 데이터 갱신
def process(x, y, index):
    # (x, y)의 위치와 연결된 나라(연합) 정보를 담는 리스트
    united = []
    united.append((x, y))
    # 너비 우선 탐색 (BFS)을 위한 큐 라이브러리 사용
    q = deque()
    q.append((x, y))
    union[x][y] = index # 현재 연합의 번호 할당
    summary = graph[x][y] # 현재 연합의 전체 인구 수
    count = 1 # 현재 연합의 국가 수
    # 큐가 빌 때까지 반복(BFS)
    while q:
        x, y = q.popleft()
        # 현재 위치에서 4가지 방향을 확인하며
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            # 바로 옆에 있는 나라를 확인하여
            if 0 <= nx < n and 0 <= ny < n and union[nx][ny] == -1:
                # 옆에 있는 나라와 인구 차이가 L명 이상, R명 이하라면
                if l <= abs(graph[nx][ny] - graph[x][y]) <= r:
                    q.append((nx, ny))
                    # 연합에 추가하기
                    union[nx][ny] = index
                    summary += graph[nx][ny]
                    count += 1
                    united.append((nx, ny))
    # 연합 국가끼리 인구를 분배
    for i, j in united:
        graph[i][j] = summary // count

total_count = 0

# 더 이상 인구 이동을 할 수 없을 때까지 반복
while True:
    union = [[-1] * n for _ in range(n)]
    index = 0
    for i in range(n):
        for j in range(n):
            if union[i][j] == -1: # 해당 나라가 아직 처리되지 않았다면
                process(i, j, index)
                index += 1
    # 모든 인구 이동이 끝난 경우
    if index == n * n:
        break
    total_count += 1

# 인구 이동 횟수 출력
print(total_count)
```

## 9. 블록 이동하기
---
[문제 클릭](https://programmers.co.kr/learn/courses/30/lessons/60063){: target="_blank"}  

### 풀기전 알아야할 것
+ __두개 이상의 좌표를 갖고 방문처리를 체크할 경우, 집합 자료구조__ 를 사용해야 한다.
    - 집합 자료구조는 순서를 기억하지 않으므로 리스트 안에 집합 자료구조로 좌표를 저장해두면, 방문여부를 확인할 때 해당 집합 안에 있는 요소의 순서와 관계없이 찾을 수 있다.
    - 예를 들면, [{(1,2),(2,3)}] 이 있다면 {(2,3),(1,2)} 로 찾을 수 있다는 의미이다.
+ __set의 인자로 넘기게되면 겉에 괄호가 벗겨지고 {}로 교체된다.__
    - ((1,2),(2,3))의 경우 set의 인자로 넘기면 {(1,2),(2,3)}으로 변환된다.
    - __참고로 list, set, deque 모두 인자로 넘긴 것은 껍때기가 벗겨지고 해당 자료구조로 감싸게 된다.__


### 내가 작성한 코드
이동 시간이 모두 1이므로 BFS를 생각해내야 한다.  
BFS는 가장 먼저 꺼내게 되는 것(가장 먼저 도착한 경우)이 가장 빠르게 도착하는 경우인 것을 기억하자.
```python
from collections import deque


def possibleWay(board, pos, n):
    way = []
    x1, y1 = pos[0]
    x2, y2 = pos[1]
    dx = [-1, 0, 1, 0]
    dy = [0, 1, 0, -1]

    # 4방향 이동
    for i in range(4):
        px1 = x1 + dx[i]
        py1 = y1 + dy[i]
        px2 = x2 + dx[i]
        py2 = y2 + dy[i]

        # 범위 내에 존재하는지
        if 0 <= px1 and px1 < n and 0 <= py1 and py1 < n and 0 <= px2 and px2 < n and 0 <= py2 and py2 < n:
            # 이동 후 좌표가 비어있는지
            if board[px1][py1] == 0 and board[px2][py2] == 0:
                way.append({(px1, py1), (px2, py2)})

    # 회전
    # 가로 방향
    if x1 == x2:
        for i in [1, -1]:
            px1 = x1 + i
            px2 = x2 + i
            # 범위 내
            if 0 <= px1 and px1 < n and 0 <= px2 and px2 < n:
                # 이동 후 좌표 비어있는지
                if board[px1][y1] == 0 and board[px2][y2] == 0:
                    way.append({(x1, y1), (x1 + i, y1)})
                    way.append({(x2, y2), (x2 + i, y2)})

    # 세로방향
    else:
        for i in [1, -1]:
            py1 = y1 + i
            py2 = y2 + i

            # 범위 내
            if 0 <= py1 and py1 < n and 0 <= py2 and py2 < n:
                # 이동 후 좌표 비었는지
                if board[x1][py1] == 0 and board[x2][py2] == 0:
                    way.append({(x1, y1), (x1, y1 + i)})
                    way.append({(x2, y2), (x2, y2 + i)})

    return way


def solution(board):
    n = len(board)
    q = deque()
    q.append((0, [(0, 0), (0, 1)]))
    positions = [{(0, 0), (0, 1)}]
    while q:
        time, pos = q.popleft()
        ways = possibleWay(board, pos, n)
        for way in ways:
            if (n - 1, n - 1) in way:
                return time + 1
            if way not in positions:
                positions.append(way)
                q.append((time + 1, list(way)))
```


### 모범 답안
다소 복잡해 보이지만 전형적인 BFS 문제 유형이다. 문제에서 로봇이 존재할 수 있는 각 위치(각 칸)을 노드로 보고, 인접한 위치와 비용이 1인 간선으로 연결되어 있다고 볼 수 있다. 좀 더 쉽게 생각한다면 현재 위치에서 모든 이동경로에 1초가 소요되는 것이다. 그렇다면 현재 위치에서 주어진 위치까지 이동하는 최소 거리 즉, 최소 시간을 구하는 것이다. 여기서 모든 이동 거리가 1(1초)인 상태에서의 최소 이동 거리라는 점에서 BFS를 이용한 풀이를 생각해내야 한다. 2번에서도 설명했듯이, __비용이 1인 경우 시작지점에서 연결되어 있는 차례대로 비용을 계산하여 그 자체가 최소거리이다.__  
다만, 이문제가 일반적인 BFS와 다른 점은, 로봇이 차지하고 있는 위치가 두 칸이며 회전을 통해 이동할 수 있다는 점이다. 그렇다면 현재 위치에서 이동할 수 있는 모든 위치를 시간정보와 같이 큐에 넣으면 되는데 이때, 위치정보는 튜플로 처리하고 집합 자료형으로 관리하는 것이 좋다. __파이썬에서 {(1,1),(1,2)}와 {(1,2),(1,1)}은 같은 집합 객체로 처리되기 때문에 집합 자료형으로 관리하면 중복 방문을 쉽게 걸러낼 수 있다.__  
```python
from collections import deque

# 시계방향
dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]


# 현재 위치에서 이동 가능한 위치
# 가능한 위치 좌표를 반환
def possible_ways(pos, board):
    possible_pos = []
    # 언팩하기 위해 리스트로 형변환
    pos = list(pos)
    pos_x1, pos_y1, pos_x2, pos_y2 = pos[0][0], pos[0][1], pos[1][0], pos[1][1]
    # 시계방향 움직임
    for i in range(4):
        px1 = pos_x1 + dx[i]
        py1 = pos_y1 + dy[i]
        px2 = pos_x2 + dx[i]
        py2 = pos_y2 + dy[i]
        if board[px1][py1] == 0 and board[px2][py2] == 0:
            possible_pos.append({(px1, py1), (px2, py2)})
    # 회전방향 움직임
    # 가로위치에 있을때
    if pos_x1 == pos_x2:
        # 위로회전, 아래로회전
        for i in [-1, 1]:
            if board[pos_x1 + i][pos_y1] == 0 and board[pos_x2 + i][pos_y2] == 0:
                possible_pos.append({(pos_x1, pos_y1), (pos_x1 + i, pos_y1)})
                possible_pos.append({(pos_x2, pos_y2), (pos_x2 + i, pos_y2)})
    # 세로위치에 있을 때
    elif pos_y1 == pos_y2:
        # 왼쪽회전, 오른쪽 회전
        for i in [-1, 1]:
            if board[pos_x1][pos_y1 + i] == 0 and board[pos_x2][pos_y2 + i] == 0:
                possible_pos.append({(pos_x1, pos_y1), (pos_x1, pos_y1 + i)})
                possible_pos.append({(pos_x2, pos_y2), (pos_x2, pos_y2 + i)})
    return possible_pos


# 위치이동 문제에서 보면 대부분 주어진 범위를 넘어가는 부분을
# 걸러줘야한다. 이런 경우 코드가 약간 길어지는데
# 이걸 막기위해서 주어진 범위보다 4면에 1줄씩 추가해서 1로 넣어주면서
# 벽을 세워주면 코드를 줄여줄 수 있다.
def solution(board):
    n = len(board)
    # 방문리스트가 필요한 이유는 최단 거리 이후에도 방문하는 경우가 있음
    # 그 경우에는 처리를 하지 않기 위해서 방문 일지가 필요함
    visited = []
    # 4면에 벽을 1로 세운 보드
    new_board = [[1] * (n + 2) for _ in range(n + 2)]

    # 보드 옮기기
    for i in range(1, n + 1):
        for j in range(1, n + 1):
            new_board[i][j] = board[i - 1][j - 1]

    # 로봇의 현재 위치
    pos = {(1, 1), (1, 2)}
    visited.append(pos)

    # 큐에 위치와 시간 삽입
    q = deque()
    q.append((pos, 0)) # q = deque([(pos, 0)]) # 한번에 하려면 append에 넣는 형태에 [] 붙여주면 된다.

    while q:
        pos, cnt = q.popleft()
        if (n, n) in pos:
            return cnt
        for possible_way in possible_ways(pos,new_board):
            # 방문한 적이 없다면
            if possible_way not in visited:
                # 방문처리와 큐 삽입
                visited.append(possible_way)
                q.append((possible_way, cnt + 1))
    return 0 # 도달 못했음
```  

### BFS/DFS 문제 풀면서 느낀점
+ 문제가 복잡할 수록 기능에 따라 함수를 각각 만들어 주는 것이 좋다.
+ 게임 보드판같은 좌표 문제는 dfs나 bfs으로 풀이할 수 있는 문제가 대부분이다. 만약 보드판에서 여러 갈래 길이 존재하고, 이동에 따른 비용이 1이면서 특정 위치까지의 최소거리를 구하는 문제라면 BFS를 우선적으로 고려해야 한다. 왜냐하면 모든 이동 비용이 1로 동일하다면 bfs에서 꺼낸 값이 가장 최소비용이기 때문이다.
+ 보드판 문제에서 쉬운 문제의 경우 1칸만을 차지하면서 이동한다. 이 경우에는 해당 위치의 값을 수정(방문처리)하면서 진행하면 무난하게 해결할 수 있다. 하지만 2칸 이상을 차지하는 경우는 다른 방법을 사용해야 한다. 뱀 같이 꼬리를 줄이는 경우라면 모든 위치를 큐에 넣어서 하나씩 빼내는 형태로 설계하면 되고, 몸의 크기가 두 칸 이상인 경우에서 물체의 모든 방향을 고려해야 한다면 방향을 움직일 때마다 해당 위치를 {}집합으로 묶어서 저장하는 것이 좋다. 집합으로 저장할 경우 파이썬에서 {(1,1),(1,2)}와 {(1,2),(1,1)}은 같은 집합 객체로 처리되기 때문에 집합 자료형으로 관리하면 중복 방문을 쉽게 걸러낼 수 있다.
+ 보드판 문제에서 문제에서 대부분 보드판 범위 내에서 한 번 거르고 이동가능한 공간인지 아닌지에서 한 번 거르게 된다. 보통 for문으로 4번 돌려서 이 과정을 수행한다. 하지만 9번의 경우는 회전의 경우까지 고려해야되서 2번 거르는 과정을 여러 번 작성해야 한다. 이 과정을 줄이기 위해서는 새로운 보드를 선언해서 가장자리의 모든 면을 1로 둘러쌓아주고 새로 만든 보드로 코딩을 이어나가는게 좋다. 이렇게 새로 만든 보드를 사용할 경우 범위내로 걸러내지 않고 벽으로 걸러내면 되기 때문에 한 번에 처리할 수 있다. 
    - 즉, 4방향 움직임이 있을 때는 그냥 그대로 사용해도 별 상관 없지만, 4방향 움직임에 회전까지 더해지면 새로운 보드를 사용해서 코딩하는게 편하다. 새로운 보드판을 사용할 경우 1,1이 시작점이다.
+ 집합을 언팩하기 위해서는 리스트로 형변환 해줘야 한다.
+ deque를 따로 선언하고 append로 추가했는데 한 번에 하고 싶으면 q = deque([])의 형태로 사용하면 된다. 즉, append의 인자로 넣었던 것에 []를 붙여서 deque의 인자로 주면 된다.

<br>

---
__본 포스팅은 '이것이 코딩 테스트다 with 파이썬'을 읽고 공부한 내용을 바탕으로 작성하였습니다.__
