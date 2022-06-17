---
layout: post
title:  구현 기출문제
subtitle:   구현 기출문제
categories: algorithm
tags: algorithm-intermediate
comments: true
# header-img:
---
* 
{:toc}

## 1. 구현이란?
---
머릿속에 있는 알고리즘을 정확하고 빠르게 프로그램을 작성하는 과정을 구현이라고 한다. 동일한 알고리즘이라면 더 간결하고 효율적으로 작성한 코드가 잘 작성된 코드이므로, 무네 핵셜 아이디어를 떠올리는 것과 별개로 구현 능력은 코딩 테스트뿐만 아니라 실무에서도 중요하다.  
구현 능력이 요구되는 대표적인 알고리즘 문제 유형으로는 완전 탐색과 시뮬레이션이 있다. 완전 탐색은 모든 경우의 수를 빠짐없이 다 계산하는 해결 방법을 의미하고, 시뮬레이션은 문제에서 제시하는 논리나 동작 과정을 그대로 코드로 옮겨야 하는 유형을 의미한다.  
완전 탐색 문제는 모든 경우의 수를 다 계산해야 하기 때문에 반복문 혹은 재귀 함수를 적절히 사용하며 예외 케이스를 모두 확인해야 하는 경우가 많다. 그러므로 일반적으로 DFS/BFS 알고리즘을 이용해서 해결한다. 시뮬레이션 문제 또한 문제에서 요구하는 복잡한 구현 요구 사항을 그대로 코드로 옮겨야 한다는 점에서 해결 방법이 비슷하다.  
원소를 나열하는 모든 경우의 수를 고려하는 상황에서 보통 순열이나 조합 라이브러리를 사용해야 한다. 이때는 파이썬 라이브러리 itertools로 쉽게 구현할 수 있다.  
<br>

## 2. 럭키 스트레이트
---
게임 내 럭키 스트레이트 라는 기술이 있다. 이는 게임 내에서 점수가 특정 조건을 만족할 때만 사용할 수 있다. 특정 조건이란 현재 캐릭터의 점수를 N이라고 할 때 자릿수를 기준으로 점수 N을 반으로 나누어 왼쪽 부분의 각 자릿수의 합과 오른쪽 부분의 각 자릿수의 합을 더한 값이 동일한 상황을 의미한다. 예를 들어 123,402가 현재 점수라면 왼쪽은 1 + 2 + 3 오른쪽은 4 + 0 + 2이므로 합이 6으로 동일하여 기술을 쓸 수 있게 된다.  
현재 점수 N이 주어지면 럭키 스트레이트를 사용할 수 있는 상태인지 아닌지 알려주는 프로그램을 작성하시오.  
__입력 조건__  
+ 첫째 줄에 점수 N이 정수로 주어진다.(10<=N<=99,999,999) 단, 점수 N의 자리수는 항상 짝수이다.

__출력 조건__  
+ 첫째 줄에 럭키 스트레이트를 사용할 수 있다면 "LUCKY", 없다면 "READY"를 출력

```
입력 예시
123402

출력 예시
LUCKY
```
<br>

### 내가 작성한 코드
```python
n = list(map(int,input())
mid =len(n)//2
left = n[:mid]
right = n[mid:]

if sum(left) == sum(right):
    print("LUCKY")
else :
    print("READY")
```
<br>

## 3. 문자 재정렬
---
알파벳 대문자와 숫자(0~9)로만 구성된 문자열이 입력으로 주어진다. 이때 모든 알파벳을 오름차순으로 정렬하여 이어서 출력한 뒤에, 그 뒤에 모든 숫자를 더한 값을 이어서 출력한다. 예를 들어 K1KA5CB7이라는 값이 들어오면 ABCKK13을 출력한다.  
__입력 조건__  
+ 첫째 줄에 하나의 문자열 S가 주어진다. (1<=S의 길이 <=10,000)

__출력 조건__  
+ 첫째 줄에 문제에서 요구하는 정답을 출력한다.

```
입력 예시
AJKDLSI412K4JSJ9D

출력 예시
ADDIJJJKKLSS20
```
<br>

### 내가 작성한 코드
```python
ls = input()
alpha =[]
tot = 0
for data in ls:
    if data.isalpha():
        alpha.append(data)
    else:
        tot+=int(data)
alpha.sort()

print(*alpha,sep="",end="")
print(tot)
```
<br>

## 모범 답안
```python
data = input()
result =[]
value =0

# 문자를 하나씩 확인하며
for x in data:
    if x.isalpha():
        result.append(x)
    else :
        value +=int(x)

# 알파벳 오름차순 정렬
result.sort()
if value !=0:
    result.append(str(value))

print(''.join(result))
```
join은 문자리스트에만 사용할 수 있으므로 합한 숫자를 삽입할 때 str로 형변환 시켜줘야 한다.
<br>

## 4. 문자열 압축
---
[문제 클릭](https://programmers.co.kr/learn/courses/30/lessons/60057){: target="_blank"}  

### 내가 작성한 코드
```python
# 알파벳 길이가 1, 1000 사이 소문자로만 존재
# 복잡도는 크게 문제될게 없어보임
# 길이별로 실제로 진행해서 짧은 길이를 담아두고 반환
def solution(s):
    length = len(s)
    answer = length

    for cut in range(1, length // 2 + 1):
        idx = 0  # 인덱스
        cnt = 1  # 반복 카운트
        tmp_length = length  # 현재 cut만큼 잘라서 줄인 문자열의 최종 길이

        # 반복 작업
        while idx + cut * 2 <= length:
            if s[idx:idx + cut] == s[idx + cut:idx + cut * 2]:
                cnt += 1
            else:
                if cnt >= 2:
                    tmp_length += len(str(cnt)) - cut * (cnt - 1)
                cnt = 1
            idx += cut

        # 마지막에 cnt 남아있는 경우 처리
        if cnt >= 2:
            tmp_length += len(str(cnt)) - cut * (cnt - 1)
        
        # 최소 길이 갱신
        answer = min(answer, tmp_length)

    return answer
```
제한사항으로 길이가 크지 않으므로 일일이 확인하는 형태로 설계했다.
<br>

2차 리뷰 코드
```python
def solution(s):
    n = len(s)  # 길이
    result = n
    # 끝에 길이 남는건 나중에 생각
    for i in range(1, n // 2 + 1):  # 자를 길이
        cnt = 1
        answer = ""
        j = 0
        while j < n : # 비교시작점이 길이를 넘어설때까지 해야 남아있는거 다 처리가능
            if s[j:j + i] == s[j + i:j + 2 * i]:
                cnt += 1
            else:
                if cnt>1:
                    answer += str(cnt)
                answer += s[j:j + i]
                cnt=1
            j += i

        result = min(result, len(answer))
    return result
```
__파이썬의 경우 리스트의 인덱스의 시작지점이 리스트 범위 안에만 있으면 끝지점이 인덱스를 넘어가도 상관없다.__  
예를 들어, ls = [1,2,3,4] 에서 ls[2:10]을 해도 알아서 짤리고 끝지점까지 나오게 된다.  
코딩할 때 유용하니 알아두자.


### 모범 답안
입력으로 주어지는 문자열의 길이가 1,000 이하이기 때문에 가능한 모든 경우의 수를 탐색하는 완전 탐색을 수행할 수 있다. 예를 들어 길이가 N인 문자열이 입력되었다면 1부터 N/2까지의 모든 수를 단위로 하여 문자열을 압축하는 방법을 모두 확인하고, 가장 짧게 압축되는 길이를 출력하면 된다.
```python
def solution(s):
    answer = len(s)
    # 1개 단위 step부터 압축 단위를 늘려가며 확인
    for step in range(1,len(s)//2+1):
        compressed= ""
        prev = s[0:step] # 앞에서부터 step까지 추출
        count =1
        # step 만큼 증가시켜가며 이전 문자열과 비교
        # 인덱싱의 경우 out of index에 대해서는 무시되므로 참고하자
        for j in range(step,len(s),step):
            if prev == s[j:j+step]:
                count+=1
            else :
                compressed += str(count)+prev if count>=2 else prev
                prev = s[j:j+step]
                count=1
                
        # 남은 문자열 처리 (if문 앞의 경우는 딱 떨여졌을경우에 해당된다)
        compressed += str(count)+prev if count>=2 else prev
        answer = min(answer,len(compressed))
    return answer
```
<br>

## 5. 자물쇠와 열쇠
---
[문제 클릭](https://programmers.co.kr/learn/courses/30/lessons/60059){: target="_blank"}  

### 내가 작성한 코드
```python
import copy


# 그래프 확장
def extendGraph(graph, lock, n):
    for i in range(n):
        for j in range(n):
            graph[i + n][j + n] = lock[i][j]


def insertKey(graph, key, i, j, m):
    for x in range(m):
        for y in range(m):
            graph[x + i][y + j] += key[x][y]


def check(graph, n):
    for i in range(n, n * 2):
        for j in range(n, n * 2):
            if graph[i][j] != 1:
                return False
    return True


def rotate(key, m):
    tmp = [[0] * m for _ in range(m)]
    for i in range(m):
        for j in range(m):
            tmp[j][m - i - 1] = key[i][j]

    return tmp


def solution(key, lock):
    n = len(lock)
    m = len(key)

    graph = [[0] * (3 * n) for _ in range(3 * n)]

    extendGraph(graph, lock, n)
    
    for i in range(2 * n):
        for j in range(2 * n):
            rotateKey = copy.deepcopy(key)
            # 4회전
            for k in range(4):
                tmp_graph = copy.deepcopy(graph)
                rotateKey = rotate(rotateKey, m)
                insertKey(tmp_graph, rotateKey, i, j, m)
                if check(tmp_graph,n):
                    return True
    return False
```


### 모범 답안
우리가 해야 할 일은 열쇠를 적당히 회전하고 이동시켜 자물쇠의 홈에 딱 맞게 끼워 넣는 것이다. 자물쇠와 열쇠의 크기는 20 * 20 보다 작다. 모든 원소에 접근할 때는 400만큼의 연산이 필요할 것이다. 코딩 테스트 채점 환경에서는 1초에 2,000만에서 1억정도의 연산을 처리할 수 있다. 즉, 범위가 매우 작으므로 복잡도를 고려하지 않아도 될 수준이다. 그렇기 때문에, 완전 탐색을 이용해서 열쇠를 이동이나 회전시켜서 자물쇠에 끼워보는 작업을 전부 시도해도는 접근 방법을 이용해 볼 수 있다. 완전 탐색을 수월하게 하기 위해서 자물쇠 리스트의 크기를 3배 이상으로 변경하면 계산이 수월해진다. 예를 들어 열쇠와 자물쇠가 3 * 3 크기라고 가정하자. 이때 가장 먼저 자물쇠를 크기가 3배인 새로운 리스트로 만들어 중앙 부분으로 옮긴다. 이제 열쇠 배열을 왼쪽 위부터 시작해서 한 칸씩 이동하는 방식으로 차례대로 자물쇠의 모든 홈을 채울 수 있는지 확인하면 된다. 자물쇠 리스트에 열쇠 리스트의 값을 더한 뒤에, 자물쇠 부분의 모든 결과값이 1이 되면 홈 모두를 채운 것이라고 볼 수 있다. 여기서 2차원 리스트의 회전 결과값을 반환하는 함수를 사용해야하는데 가끔씩 사용되므로 알아두도록 하자.
```python
# 2차원 리스트 90도 회전
def rotate_a_matrix_by_90_degree(a):
    x = len(a)  # 행의 길이 계산
    y = len(a[0])  # 열의 길이 계산

    # 회전하는 결과 리스트는 행과 열의 길이가 바뀐다.
    # 기존에는 x*y 였다면 회전 후에는 y*x가 된다.
    result = [[0] * x for _ in range(y)]

    # 회전한 리스트의 인덱스는 거꾸로되어 y,x로 관여한다.
    for i in range(x):
        for j in range(y):
            # result[y-j-1][i] = a[i][j]# 왼쪽으로 회전
            result[j][x - i - 1] = a[i][j]  # 오른쪽으로 회전
    return result


# 자물쇠 부분이 모두 1인지 확인
def check(new_lock):
    lock_len = len(new_lock) // 3
    for i in range(lock_len, lock_len * 2):
        for j in range(lock_len, lock_len * 2):
            if new_lock[i][j] != 1:
                return False
    return True
    # if total == lock_len*lock_len:
    #     return True
    # else :
    #     return False


def solution(key, lock):
    n = len(lock)
    m = len(key)
    # 알고리즘 설계를 자물쇠 리스트와 키 리스트의 값의 합이 모두 1이되는 경우 완성
    # 비교를 편하게 하기 위해서 원래 자물쇠 크기의 3배로 새로운 리스트 생성
    new_lock = [[0]*(n*3) for _ in range(n*3)]

    # lock를 new_lock의 중앙으로 옮기기
    for i in range(n):
        for j in range(n):
            new_lock[n+i][n+j]=lock[i][j]

    # 4가지 방향에 대한 확인
    for _ in range(4):
        key = rotate_a_matrix_by_90_degree(key)
        # new_lock의 비교 시작 좌표
        for x in range(n*2): # 1부터 해도 되나 시간의 차이는 거의 없으므로 편의상
            for y in range(n*2):
                # key의 비교 좌표, 자물쇠에 열쇠 넣기
                for a in range(m):
                    for b in range(m):
                        new_lock[x+a][y+b] += key[a][b]
                # 채워졌는지 확인
                if check(new_lock):
                    return True
                # 다시 key 빼내기
                for a in range(m):
                    for b in range(m):
                        new_lock[x+a][y+b] -= key[a][b]
    return False
```

### 회전하기
배열을 시계, 반시계 방향으로 회전하는 코드가 종종 나온다고 하니 익혀두도록 하자
```python
# 시계 방향
def rotate(key):
    x = len(key)
    y = len(key[0])
    ls = [[0] * x for _ in range(y)]

    for i in range(x):
        for j in range(y):
            # 시계
            ls[j][x-1-i] = key[i][j]
            # 반시계
            #ls[y-1-j][i] = key[i][j]
    return ls

print(rotate([[0, 0, 0], [1, 0, 0], [0, 1, 1]]))
```

<br>

## 6. 뱀
---
[문제 클릭](https://www.acmicpc.net/problem/3190){: target="_blank"}  


### 내가 작성한 코드
```python
n = int(input())
k = int(input())

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]

graph = [[0] * n for _ in range(n)]
direction = []  # 방향 전환점
snake = [(0, 0)]  # 뱀이 차지하고 있는 좌표

# 사과 정보 입력
for _ in range(k):
    x, y = map(int, input().split())
    graph[x - 1][y - 1] = 1

# 방향 전환 입력
l = int(input())
for _ in range(l):
    num, way = input().split()
    direction.append((int(num), way))

# 첫 시작 조건 초기화
way = 1
cnt = 0
x = y = 0

while True:
    cnt += 1
    x += dx[way]
    y += dy[way]

    # 범위 바깥으로 이동
    if x < 0 or x >= n or y < 0 or y >= n:
        break

    # 충돌
    if (x, y) in snake:
        break

    # 사과 없으면 길이 줄이기
    if graph[x][y] == 0:
        snake.pop(0)
    # 사과 있으면 사과 없애기
    else:
        graph[x][y] = 0

    # 방문처리
    snake.append((x, y))

    if direction and cnt == direction[0][0]:
        d = direction.pop(0)[1]
        if d == 'D':
            way = (way + 1) % 4
        else:
            way = (way - 1 + 4) % 4

print(cnt)
```
파이썬의 경우 c++랑 나눗셈 연산이 달라서 조금 신경써야하는 경우가 있는데 고려하고 싶지 않다면 나누는 값만큼 우선 더해주고 그 값을 나눠주면 문제가 없다.  
파이썬은 유클리드 나눗셈 방식을 따르는데 쉽게 생각하면 내림을 한다고 생각하면 된다. 위에서 사용한 것으로 예시를 들어보면 만약 way가 -1로 된다면 원래 의도대로라면 서쪽 3의 값을 가져야 한다. -1//4의 값은 -0.25로 -1의 몫을 가지게 되고 이에따라 나머지는 -1을 만들기 위해서는 4*-1 + 3이므로 나머지는 3이된다.
```python
-2018/5 == -403.6 

# 여기서 몫의 나눗셈을 하면 파이썬은 내림하여 계산한다.
# 따라서 음수의 경우 정수부가 바뀐다.
-2018 // 5  == -404

# 나머지 연산
# -8//3 은 -3이다 따라서 3*-3 -> -9 에서
# -8을 만들려면 1을 더해주면 되므로 나머지는 1이다
-8 % 3 == 1

# -7//3 은 -3이다 따라서 -3*3 -> 9에서
# -7을 만들려면 2를 더해줘야하므로 나머지는 2이다
-7 % 3 == 2

# -7 // -3 == 2이다 따라서 -3*2 -> -6
# -7을 만들려면 -1을 더하면 되므로 나머지는 -1이다
-7 % -3 == -1

# -8 // -3 == 2이다 따라서 -3*2 -> -6
# -8을 만드려면 -2를 더하면 되므로 나머지는 -2이다
-8 % -3 == -2
```


### 모범 답안
2차원 배열상의 특정 위치에서 동,남,서,북의 위치로 이동하는 기능을 구현해야 한다. 이 문제의 경우, 뱀이 처음에 오른쪽(동쪽)을 바라보고 있다는 점을 고려하자. 더불어 뱀의 머리가 뱀의 몸에 닿는 경우 종료해야 하므로, 매 시점마다 뱀이 존재하는 위치를 항상 2차원 리스트에 기록해야 한다.  
이러한 시뮬레이션 문제 유형을 가장 쉽게 풀기 위해서는 그림으로 그려보는 것이 좋다. 
```python
n = int(input())
k = int(input())
data = [[0] * (n + 1) for _ in range(n + 1)] # 맵 정보
info = [] # 방향 회전 정보

# 맵 정보(사과 있는 곳은 1로 표시)
for _ in range(k):
    a, b = map(int, input().split())
    data[a][b] = 1

# 방향 회전 정보 입력
l = int(input())
for _ in range(l):
    x, c = input().split()
    info.append((int(x), c))

# 처음에는 오른쪽을 보고 있으므로(동, 남, 서, 북)
dx = [0, 1, 0, -1]
dy = [1, 0, -1, 0]

def turn(direction, c):
    if c == "L":
        direction = (direction - 1) % 4
    else:
        direction = (direction + 1) % 4
    return direction

def simulate():
    x, y = 1, 1 # 뱀의 머리 위치
    data[x][y] = 2 # 뱀이 존재하는 위치는 2로 표시
    direction = 0 # 처음에는 동쪽을 보고 있음
    time = 0 # 시작한 뒤에 지난 '초' 시간
    index = 0 # 다음에 회전할 정보
    q = [(x, y)] # 뱀이 차지하고 있는 위치 정보(꼬리가 앞쪽)

    while True:
        nx = x + dx[direction]
        ny = y + dy[direction]
        # 맵 범위 안에 있고, 뱀의 몸통이 없는 위치라면
        if 1 <= nx and nx <= n and 1 <= ny and ny <= n and data[nx][ny] != 2:
            # 사과가 없다면 이동 후에 꼬리 제거
            if data[nx][ny] == 0:
                data[nx][ny] = 2
                q.append((nx, ny))
                px, py = q.pop(0)
                data[px][py] = 0
            # 사과가 있다면 이동 후에 꼬리 그대로 두기
            if data[nx][ny] == 1:
                data[nx][ny] = 2
                q.append((nx, ny))
        # 벽이나 뱀의 몸통과 부딪혔다면
        else:
            time += 1
            break
        x, y = nx, ny # 다음 위치로 머리를 이동
        time += 1
        if index < l and time == info[index][0]: # 회전할 시간인 경우 회전
            direction = turn(direction, info[index][1])
            index += 1
    return time

print(simulate())
```
<br>

## 7. 기둥과 보 설치
---
[문제 클릭](https://programmers.co.kr/learn/courses/30/lessons/60061){: target="_blank"}  


### 내가 작성한 코드
```python
def canInstall(answer, x, y, a):
    # 기둥
    # 해당 좌표가 바닥이거나
    # 해당 좌표 아래 기둥이 있거나
    # 해당 좌표 아래 보가 있거나

    if a == 0:
        if y==0 or [x,y-1,0] in answer or [x-1,y,1] in answer or [x,y,1] in answer:
            return True
    # 보
    # 좌표 아래 기둥이 있거나
    # 좌표 오른쪽 아래 기둥이 있거나
    # 좌표 왼쪽과 오른쪽에 보가 있다면
    else:
        if [x,y-1,0] in answer or [x+1,y-1,0] in answer or ([x-1,y,1] in answer and [x+1,y,1] in answer):
            return True

    return False

def canDelete(answer):    
    for x,y,a in answer:
        if not canInstall(answer,x,y,a):
            return False
    return True


def solution(n, build_frame):

    answer =[]
   
    for x,y,a,b in build_frame:
        # 설치
        if b == 1 and canInstall(answer, x, y, a):
            answer.append([x,y,a])

        # 삭제
        elif b==0 :
            answer.remove([x, y, a])
            if not canDelete(answer):
                answer.append([x,y,a])

    answer.sort()

    return answer
```
+ 기둥 보를 우선으로 나눌지, 설치 삭제를 우선으로 나눌지 -> 삭제는 어느 경우나 같음 -> 설치 삭제로 나누기
+ 설치 가능한지 확인하는 함수와 삭제 가능한지 확인하는 함수 두 개로 분리
+ 설치의 경우는 조건 그대로 설계하면 되고, 삭제의 경우는 일단 answer에서 제거한 뒤 answer에 담긴 내용들의 구조가 깨지지 않았는지 확인하는 방식으로 해결



### 모범 답안
전체 명령의 개수는 총 1,000개 이하이다. 따라서 O(N^2)으로 해결하는 것이 이상적이나 시간제한이 5초로 넉넉하기 때문에 O(N^3)의 알고리즘을 이용해도 정답판정을 받을 수 있다. 따라서 후자로 해결하는 가장 간단한 방법은, 설치 및 삭제 연산을 요구할 때마다 일일이 전체 구조물을 확인하며 규칙을 확인하는 것이다. 이렇게 복잡한 문제의 경우 해결에 따른 함수를 따로 만들어 사용하는 것이 좋다.
```python
# 현재 설치된 구조물이 가능한 구조물인지 확인하는 함수
def possible(answer):
    for x, y, stuff in answer:
        if stuff == 0:  # 설치된 것이 기둥인 경우
            # 바닥 위, 보의 한쪽 끝 부분 위, 다른 기둥 위라면 정상
            if y == 0 or [x - 1, y, 1] in answer or [x, y, 1] in answer or [x, y - 1, 0] in answer:
                continue
            # 아니면
            return False
        else:  # 설치된 것이 보인 경우
            # 한쪽 끝부분이 기둥 위, 양쪽 끝 부분이 다른 보와 동시에 연결
            if [x, y - 1, 0] in answer or [x + 1, y - 1, 0] in answer or ([x - 1, y, 1] in answer and [x + 1, y, 1] in answer):
                continue
            return False
    return True


def solution(n, build_frame):
    answer = []
    for x, y, stuff, operate in build_frame:
        if operate == 0:  # 삭제
            answer.remove([x, y, stuff])  # 일단 삭제
            if not possible(answer):  # 불가능한 형태
                answer.append([x, y, stuff]) # 다시 설치
        else:  # 설치
            answer.append([x, y, stuff])  # 일단 설치
            if not possible(answer):  # 불가능한 형태
                answer.remove([x, y, stuff])  # 삭제
    return sorted(answer)
    # answer.sort()
    # return answer

# 코딩 중간에 생겼던 의문점
# 삭제의 경우 answer에서 삭제 후 모양 성립 조건에 위배되어 다시 추가했다
# 근데 맨 뒤에 추가해도 되나?
# 상관 없다 -> answer의 순서에 관계 없이 in으로 안에 있는지 없는지로 판단하기 때문
```
<br>

## 8. 치킨 배달
---
[문제 클릭](https://www.acmicpc.net/problem/15686){: target="_blank"}  

### 내가 작성한 코드
주어진 제한 조건에서 복잡도를 신경안써도 될정도로 범위가 작다. 처음에는 최소거리치킨집을 카운트할 리스트를 선언하고 각각 집에서 최소거리에 해당하는 치킨집 개수를 카운트해서 가장 적게나온 치킨집을 빼주려고 했다. 하지만 이렇게 할 경우 3번째 예시 같은 경우를 해결할 수 없다. 따라서 범위가 매우 작다는 점을 생각하여 combinations를 이용해 각 경우마다 최소거리를 구해준 뒤 min으로 비교해가는 알고리즘을 설계했다.
```python
from itertools import combinations

n, m = map(int, input().split())

INF = int(1e9)
chicks = []
homes = []
answer = INF

# 집과 치킨집 위치 찾기
for i in range(n):
    graph = list(map(int, input().split()))
    for j in range(n):
        if graph[j] == 1:
            homes.append((i + 1, j + 1))
        elif graph[j] == 2:
            chicks.append((i + 1, j + 1))

# 치킨m개 뽑기
for poses in combinations(chicks, m):
    tot = 0 # 뽑은 m개의 최소 치킨 거리 저장소
    # 각 집에 대해 최소 치킨거리 찾기
    for home in homes:
        dis = INF
        for pos in poses:
            temp = abs(home[0] - pos[0]) + abs(home[1] - pos[1])
            dis = min(dis, temp)
        tot += dis
    answer = min(answer, tot)

print(answer)
```


### 모범 답안
기존에 존재하는 치킨집을 줄여서 최대 M개로 유지하면서, 일반 집들오부터 M개의 치킨집까지의 거리를 줄이는 것이 목표다. 이후에 도시의 치킨 거리 합의 최솟값을 계산하면 된다.  
기본적으로 입력으로 들어오는 치킨집의 개수 범위를 생각해보자. 치킨집의 개수 범위는 M <= 치킨집의 개수<= 13이다. 만약 치킨집 중에서 M개를 고르는 조합을 고려한다면 경우의 수가 얼마나 많을지 생각해보자. 최대 13개에서 M개를 선택하는 조합과 동일하다. (참고로 조합은 중간값의 개수를 선택(13의 중간값 6,7)을 하는 것이 최대값이다. 16개중 선택할 때 최대가 1만을 넘기고 20에서 선택할 때 10만을 넘긴다.) M값이 뭐가 되든지 간에 13개 중에서 M개를 고르는 조합의 경우 10,000을 넘지 않고 집의 개수가 최대 100개이므로 총 연산 횟수가 1억을 넘지 못한다. 따라서 모든 경우의 수를 계산하더라도 시간 초과 없이 문제를 해결할 수 있다.

```python
from itertools import combinations
import sys

input = sys.stdin.readline
n, m = map(int, input().split())

# 지도, 일반집, 치킨집
graph = [[] for _ in range(n)]
chick = []
house = []

# 지도 작성
for i in range(n):
    graph[i] = list(map(int, input().rstrip().split()))

# 집 정보 추출
for i in range(n):
    for j in range(n):
        if graph[i][j] == 1:  # 일반집
            house.append([i, j])
        elif graph[i][j] == 2:  # 치킨집
            chick.append([i, j])

# 경우의 수
choose_lists = list(combinations(chick, m))


# 치킨 거리 최소값구하는 함수
def solution(choose_list):
    answer = 0
    for x, y in house:
        tmp = int(1e9)
        for i, j in choose_list:
            tmp = min(tmp, abs(x - i) + abs(y - j))
        answer += tmp
    return answer

tmp = int(1e9)
for choose_list in choose_lists:
    tmp = min(tmp,solution(choose_list))
print(tmp)
```

<br>

## 9. 외벽 점검
---
[문제 클릭](https://programmers.co.kr/learn/courses/30/lessons/60062){: target="_blank"}  

### 내가 작성한 코드
```python
from itertools import permutations
import copy


def solution(n, weak, dist):
    length = len(weak)
    ans = (int)(1e9)

    # 원형 1자로 두배해서 펴기
    extendWeak = copy.deepcopy(weak)
    for i in weak:
        extendWeak.append(i + n)

    # 일할 사람 수
    for workerCount in range(1, length + 1):
        # 일할 사람 수에 따른 일할 사람 뽑기
        for workers in permutations(dist, workerCount):
            # 일 시작점
            for weakIdx in range(length):
                position = weak[weakIdx] + workers[0]  # 첫 일하는 사람이 일하고난 후 위치
                cnt = 1
                workerIdx = 1

                # 나머지 점검 위치 확인
                for weakSpot in extendWeak[weakIdx + 1:weakIdx + length]:
                    if position >= weakSpot:
                        cnt += 1
                    else:
                        # 일하는 사람보다 초과시 중단
                        if workerIdx >= workerCount:
                            break
                        position = weakSpot + workers[workerIdx]
                        workerIdx += 1
                        cnt += 1

                if cnt == length:
                    ans = min(ans, workerCount)

    if ans == (int)(1e9):
        return -1
    return ans
```
조건상으로 복잡도를 무시해도 될 정도로 작다. 따라서 모든 경우에 대해 고려한다.  
주어진 취약점에서 시계방향, 반시계방향으로 가능한데 사실상 시작점만 다르게 잡으면 반시계랑 시계랑 똑같다.  
예를 들면 1에서 3만큼 반시계로 도는 것이랑 10에서 3만큼 시계로 도는 것을 결과적으로 같다.  
또한, 원형을 그대로 유지하고 진행할 경우, 10에서 3을 더하면 13으로 표기되어 나눠주어야 하기 때문에 더 복잡해진다.  
따라서, 원형을 잘라서 일자로 쭉 편다고 생각하고 점들을 2배씩 확장시킨다.  
즉, 10에다가 3을 더하면 원래는 1위치에 도착해야하지만, 확장시켜서 13에 위치에 취약지점을 또 만드는 것이다.


### 모범답안
제한 조건을 보았을 때, weak 리스트와 dist 리스트의 길이가 매우 작은 것을 알 수 있다. 따라서 주어지는 데이터의 개수가 적을 때는 모든 경우를 일일이 확인하는 완전 탐색으로 접근해볼 수 있다.  
친구를 나열하는 모든 경우의 수를 각각 확인하여 친구를 최소 몇 명 배치하면 되는지 계산하면 문제를 해결할 수 있다. (문제에서 찾고자 하는 값은 투입해야 하는 친구 수의 최솟값이다. 이때 전체 친구의 수 최대는 8이다. 모든 친구를 무작위로 나열하는 모든 순열의 개수는 8!=40,320으로 충분히 계산 가능한 경우의 수이다.)
다만, 문제에서는 취약한 지점들이 원형으로 구성되어 있다고 설명하고 있다. 이처럼 __원형으로 나열된 데이터를 처리하는 경우에는, 문제 풀이를 간단히 하기 위하여 길이를 2배로 늘려서 원형을 일자 형태로 만드는 작업을 해주면 유리하다.__  
문제에 제시된 입출력 예시 2로 확인해보자. 취약한 지점을 2배하여 일자 형태로 만들면 1, 3, 4, 9, 10, 13, 15, 16, 21, 22가 된다. 친구 나열의 경우는 3!으로 6가지가 된다. 이제 각각의 경우에 대하여 5개의 취약한 지점을 모두 검사할 수 있는지 확인하면 된다.
```python
from itertools import permutations

def solution(n, weak, dist):
    length = len(weak)    
    answer = len(dist) +1 # 친구 수 +1 나중에 수정되지 않으면 친구 투입 수 초과

    # weak 2배 일렬로 만들기
    for i in range(length):
        weak.append(n+weak[i])

    # 친구 순열 선택
    for friends in permutations(dist,len(dist)):

        # 시작 위치 설정( 0 ~ length -1)        
        for start in range(length):
            count = 1  # 첫 번째 친구 투입
            position = weak[start] + friends[count-1]
                        
            # 시작지점을 기준으로 이후 주어진 취약 갯수만큼 확인
            for index in range(start+1,start+length):
                # 다음 취약 지점에 못 미치는 경우
                if position < weak[index]:
                    count+=1 # 친구수 추가
                    # 친구 수 초과시
                    if count > len(dist):
                        break
                    position = weak[index]+friends[count-1] # 현재 위치 수정
            answer = min(count,answer)
    # 주어진 친구수보다 많을 경우 -1 리턴
    if answer > len(dist):
        return -1
    return answer
```
이 문제에서 얻어갈 점은 제한사항에서 범위가 매우 작아서 복잡도를 고려안해도 될 정도면 __대부분 완전 탐색__, 일일이 확인하는 알고리즘을 설계하는 문제일 것이다. 또한, __원형에서 문제점을 카운트 하는데 시작 인덱스의 위치가 상관 없는 경우 또는 시계,반시계 이동이 가능한 경우에서는 인덱스를 고려하기 복잡해지므로 주어진 원형이 길이에서 2배를 한 뒤 일자형태로 만들어 생각하는게 더 편하다.__

<Br>

__구현 기출 느낀점__  
구현 문제는 대부분 특별한 자료구조를 사용하지 않았다. 대부분 주어진 범위가 작기때문에 모든 경우를 탐색해야했고 경우에 따라 itertools를 활용해 순열, 조합을 사용해 각각에 따른 경우를 사용해야 했다.  


<br>

---
__본 포스팅은 '이것이 코딩 테스트다 with 파이썬'을 읽고 공부한 내용을 바탕으로 작성하였습니다.__

