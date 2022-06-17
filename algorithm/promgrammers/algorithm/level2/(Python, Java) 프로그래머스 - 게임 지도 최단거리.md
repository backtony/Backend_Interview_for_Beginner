[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/1844)


## Python 풀이
```python
from collections import deque


def solution(maps):
    weight = len(maps[0])
    height = len(maps)

    q = deque()
    dx = [-1, 0, 1, 0]
    dy = [0, 1, 0, -1]

    q.append((1, 0, 0))  # cost, x, y

    while q:
        cost, x, y = q.popleft()
        if x == height - 1 and y == weight - 1:
            return cost

        for i in range(4):
            px = x + dx[i]
            py = y + dy[i]

            if 0 <= px and px < height and 0 <= py and py < weight:
                if maps[px][py] == 1:
                    maps[px][py] = -1  # 방문 처리
                    q.append((cost + 1, px, py))

    return -1
```

## Java 풀이
```java
class Solution {
    public int solution(int[][] maps) {
        int n = maps.length;
        int m = maps[0].length;
        int[] dx = {-1, 0, 1, 0};
        int[] dy = {0, 1, 0, -1};
        int answer = -1;

        // 첫 위치 방문 처리
        Queue<Log> q = new LinkedList<>();
        q.add(new Log(0, 0, 1));
        maps[0][0] = 0;

        // bfs
        while (!q.isEmpty()) {
            Log cur = q.poll();
            int x = cur.getX();
            int y = cur.getY();
            int cost = cur.getCost();

            if (x == n - 1 && y == m - 1) {
                answer = cost;
                break;
            }

            for (int d = 0; d < 4; d++) {
                int px = x + dx[d];
                int py = y + dy[d];
                if (0 <= px && px < n && 0 <= py && py < m) {
                    if (maps[px][py] == 1) {
                        maps[px][py] = 0;
                        q.add(new Log(px, py, cost + 1));
                    }
                }
            }
        }
        return answer;
    }

    class Log {
        int x;
        int y;
        int cost;

        public Log(int x, int y, int cost) {
            this.x = x;
            this.y = y;
            this.cost = cost;
        }

        public int getX() {
            return x;
        }

        public int getY() {
            return y;
        }

        public int getCost() {
            return cost;
        }
    }
}
```



