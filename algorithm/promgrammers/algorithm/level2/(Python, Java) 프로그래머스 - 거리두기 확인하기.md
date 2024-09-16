[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/81302)


## Python 풀이 1
```python
from collections import deque

def solution(places):
    answer = []

    for place in places:

        # 대기자 위치 찾기
        people = []
        for row, datas in enumerate(place):
            for column, data in enumerate(datas):
                if data == 'P':
                    people.append((row, column))

        key = 1
        for person in people:
            graph = list(map(list, place))
            key = bfs(graph, person)
            if key == 0:
                break
        answer.append(key)

    return answer

def bfs(graph, start):
    q = deque()
    dx = [-1, 0, 1, 0]
    dy = [0, 1, 0, -1]
    x, y = start
    q.append((0, x, y))  # 비용, 위치
    graph[x][y] = 1  # 방문 처리

    while q:
        cost, x, y = q.popleft()

        for i in range(4):
            px = x + dx[i]
            py = y + dy[i]

            if 0 <= px and px < 5 and 0 <= py and py < 5:
                if graph[px][py] in ['O', 'P']:
                    q.append((cost + 1, px, py))
                    if graph[px][py] == 'P' and cost + 1 <= 2:
                        return 0
                    graph[px][py] = 1  # 방문 처리
    return 1
```
문제를 읽고 그래프 문제라고 파악했다.  
모든 위치에 대한 가능한 경로는 플로이드 워셜 알고리즘이 생각났는데 플로이드 워셜 알고리즘은 각각의 간선정보가 필요하기 때문에 사용할 수 없었다.  
그 다음 생각난게 BFS이고 복잡도도 10초로 넉넉하게 주어졌기 때문에 BFS로 풀이했다.

## Python 풀이 2
```python
from itertools import combinations


def solution(places):
    answer = []

    for place in places:
        # 사람 좌표 탐색
        people = []
        for x in range(5):
            for y in range(5):
                if place[x][y] == "P":
                    people.append((x, y))
        key = 1
        for person1, person2 in combinations(people, 2):
            if not is_safe(place, person1, person2):
                key = 0
                break

        answer.append(key)

    return answer


def is_safe(place, person1, person2):
    x1, y1 = person1
    x2, y2 = person2
    distance = abs(x1 - x2) + abs(y1 - y2)
    if distance == 1:
        return False

    if distance == 2:
        if x1 == x2 and place[x1][(y1 + y2) // 2] == 'X':
            return True
        if y1 == y2 and place[(x1 + x2) // 2][y1] == 'X':
            return True
        if x1 != x2 and y1 != y2 and place[x1][y2] == 'X' and place[x2][y1] == 'X':
            return True
        return False

    return True
```
문제의 주어진 조건을 사용하여 직관적으로 풀이했다.


## Java 풀이
```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

class Solution {

    int[] dx = {-1, 0, 1, 0};
    int[] dy = {0, 1, 0, -1};

    public int[] solution(String[][] places) {
        List<Integer> answer = new ArrayList<>();

        for (String[] place : places) {
            // 사람 위치 찾기
            List<Position> people = new ArrayList<>();
            for (int x = 0; x < 5; x++) {
                for (int y = 0; y < 5; y++) {
                    if (place[x].charAt(y) == 'P') {
                        people.add(new Position(x, y));
                    }
                }
            }

            int key = 1;
            for (Position person : people) {
                boolean[][] visited = new boolean[5][5];
                if (!bfs(place, person.getX(), person.getY(), visited)) {
                    key = 0;
                    break;
                }
            }
            answer.add(key);
        }

        return answer.stream().mapToInt(Integer::intValue).toArray();
    }

    private boolean bfs(String[] place, int x, int y, boolean[][] visited) {

        Queue<Position> q = new LinkedList<>();
        q.add(new Position(x, y, 0));
        visited[x][y] = true;

        while (!q.isEmpty()) {
            Position position = q.poll();
            for (int d = 0; d < 4; d++) {
                int px = position.getX() + dx[d];
                int py = position.getY() + dy[d];

                if (0 <= px && px < 5 && 0 <= py && py < 5) {
                    if (visited[px][py] == false && place[px].charAt(py) != 'X') {
                        if (place[px].charAt(py) == 'P' && position.getCost() + 1 <= 2)
                            return false;
                        q.add(new Position(px, py, position.getCost() + 1));
                        visited[position.getX()][position.getY()] = true;
                    }
                }
            }
        }
        return true;
    }

    class Position {
        int x;
        int y;
        int cost;

        public Position(int x, int y) {
            this.x = x;
            this.y = y;
        }

        public Position(int x, int y, int cost) {
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


## kotlin 풀이
```kotlin
class Solution {
    fun solution(places: Array<Array<String>>): IntArray {

        val answer = mutableListOf<Int>()

        places.forEach places@{ place ->
            val peoples = mutableListOf<Position>()

            place.forEachIndexed { y, row ->
                row.forEachIndexed { x, c ->
                    if (c == 'P') {
                        peoples.add(Position(x, y, 0))
                    }
                }
            }

            // bfs
            for (person in peoples) {
                val result = bfs(person, place)
                if (result == false) {
                    answer.add(0)
                    return@places
                }
            }

            answer.add(1)
        }

        return answer.toIntArray()
    }

    private fun bfs(person: Position, place: Array<String>): Boolean {
        val visited = MutableList(5) { MutableList(5) { false } }

        val queue = mutableListOf<Position>()
        queue.add(person)

        while (queue.isNotEmpty()) {
            visited[person.y][person.x] = true
            val current = queue.removeFirst()

            val bx = listOf(1, 0, -1, 0)
            val by = listOf(0, -1, 0, 1)

            for (move in bx.zip(by)) {
                val px = current.x + move.first
                val py = current.y + move.second

                if (px in 0..4 && py in 0..4) {
                    if (visited[py][px] == false && current.distance < 2) {
                        when (place[py][px]) {
                            'O' -> {
                                queue.add(Position(px, py, current.distance + 1))
                            }

                            'P' -> {
                                return false
                            }
                        }
                    }
                }
            }
        }

        return true
    }

    data class Position(
        val x: Int,
        val y: Int,
        val distance: Int,
    )
}
```

