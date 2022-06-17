[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/86052)


## Python 풀이 1
```python
def solution(grid):
    answer = []
    weight = len(grid[0])
    height = len(grid)
    dx = [-1, 0, 1, 0]
    dy = [0, 1, 0, -1]
    edges = set()
    for x1 in range(height):
        for y1 in range(weight):
            # d 시계방향 0,1,2,3
            for d in range(4):
                x2 = (x1 + dx[d]) % height
                y2 = (y1 + dy[d]) % weight
                distance = 0
                while (x1, y1, x2, y2, d) not in edges:
                    distance += 1
                    edges.add((x1, y1, x2, y2, d))
                    x1 = x2
                    y1 = y2
                    # L R S  로 거르고 들어오는 방향에 따라 움직임이 달라짐
                    if grid[x2][y2] == 'L':
                        d = (d - 1 + 4) % 4
                    elif grid[x2][y2] == 'R':
                        d = (d + 1) % 4
                    x2 = (x2 + dx[d]) % height
                    y2 = (y2 + dy[d]) % weight

                if distance != 0:
                    answer.append(distance)

    answer.sort()

    return answer
```

## Python 풀이 2
```python
import sys
sys.setrecursionlimit(10**6)

dx = [-1, 0, 1, 0]
dy = [0, 1, 0, -1]
visited = set()

def solution(grid):
    n = len(grid)
    m = len(grid[0])
    answer = []
    for x in range(n):
        for y in range(m):
            for d in range(4):
                cnt = cycle(grid, n, m, x, y, d)
                if cnt:
                    answer.append(cnt)
    return sorted(answer)


def cycle(grid, n, m, x, y, d):
    if (x, y, d) in visited:
        return 0

    visited.add((x, y, d))

    px = (x + dx[d])%n
    py = (y + dy[d])%m

    if grid[px][py] == 'L':
        answer = cycle(grid, n, m, px, py, (d + 4 - 1) % 4)
    elif grid[px][py] == 'R':
        answer = cycle(grid, n, m, px, py, (d + 1) % 4)
    else:
        answer = cycle(grid, n, m, px, py, d)

    return answer + 1
```
파이썬에서 재귀 문제 풀 때는 반드시 recursionlimit을 세팅해주도록 한다.


## Java 풀이
```java
class Solution {
    public int[] solution(String[] grid) {
        List<Integer> answer = new ArrayList<>();
        int height = grid.length;
        int weight = grid[0].length();
        boolean[][][] visited = new boolean[height][weight][4];
        int[] dx = {-1, 0, 1, 0};
        int[] dy = {0, 1, 0, -1};

        for (int x = 0; x < height; x++) {
            for (int y = 0; y < weight; y++) {
                for (int d = 0; d < 4; d++) {
                    // 미방문
                    int cnt = 0;
                    while (!visited[x][y][d]) {
                        visited[x][y][d] = true;
                        cnt++;
                        if (grid[x].charAt(y) == 'L') {
                            d = (d - 1 + 4) % 4;
                        } else if (grid[x].charAt(y) == 'R') {
                            d = (d + 1) % 4;
                        }
                        x = (x + height + dx[d]) % height;
                        y = (y + weight + dy[d]) % weight;
                    }
                    if (cnt != 0)
                        answer.add(cnt);

                }
            }
        }
        return answer.parallelStream().sorted().mapToInt(Integer::intValue).toArray();
    }
}
```
자바의 경우는 파이썬 풀이 1번처럼 다루려면 클래스를 만들고 사용해야 하기 때문에 쉽게 접근하기 위해 boolean 배열로 방문처리를 작성했다.