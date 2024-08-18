[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/86971)


## Python 풀이
```python
from itertools import combinations


def solution(n, wires):
    answer = n
    for custom_wires in combinations(wires, len(wires) - 1):

        # init graph
        graph = [[] for _ in range(n + 1)]
        for x, y in custom_wires:
            graph[x].append(y)
            graph[y].append(x)

        visited = [0] * (n + 1)
        cur_network = dfs(graph, 1, visited)
        another_network = n - cur_network
        answer = min(answer, abs(another_network - cur_network))

    return answer


def dfs(graph, pos, visited):
    visited[pos] = 1
    cnt = 1
    for next in graph[pos]:
        if visited[next] == 0:
            cnt += dfs(graph, next, visited)

    return cnt
```
어느 간선을 끊어야 최소의 차이로 끊어내는지는 알 수 없다. 따라서 일일이 해봐야 한다.  
combination으로 간선 하나를 끊어내면 2개의 그래프가 나올 것이다.  
시작 정점을 아무 곳이나 잡아서 dfs를 돌리고 방문한 정점의 개수를 카운트 하면 (n - 방문 점점 개수)를 통해 다른 네트워크의 연결 정점 개수도 도출해낼 수 있다.  


## Java 풀이
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class Solution {
    public int solution(int n, int[][] wires) {
        int answer = n;

        int length = wires.length;
        for (int removeIdx = 0; removeIdx < length; removeIdx++) {
            Map<Integer, List<Integer>> graph = initGraph(wires, length, removeIdx);

            boolean[] visited = new boolean[n + 1];
            int curNetworkCount = dfs(graph, visited, 1);
            int anotherNetworkCount = n - curNetworkCount;

            answer = Math.min(answer, Math.abs(curNetworkCount - anotherNetworkCount));
        }

        return answer;
    }

    private Map<Integer, List<Integer>> initGraph(int[][] wires, int length, int removeIdx) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        for (int idx = 0; idx < length; idx++) {
            if (idx == removeIdx)
                continue;

            int x = wires[idx][0];
            int y = wires[idx][1];
            addOppositePosition(graph, x, y);
            addOppositePosition(graph, y, x);
        }
        return graph;
    }

    private void addOppositePosition(Map<Integer, List<Integer>> graph, int x, int y) {
        List<Integer> values1 = graph.getOrDefault(x, new ArrayList<>());
        values1.add(y);
        graph.put(x, values1);
    }


    private int dfs(Map<Integer, List<Integer>> graph, boolean[] visited, int pos) {
        visited[pos] = true;

        int cnt = 1;
        for (Integer next : graph.getOrDefault(pos, new ArrayList<>())) {
            if (visited[next] == false)
                cnt += dfs(graph, visited, next);
        }
        return cnt;
    }
}
```

## kotlin 풀이
```kotlin
import kotlin.math.absoluteValue
import kotlin.math.min

class Solution {
    fun solution(n: Int, wires: Array<IntArray>): Int {
        var answer: Int = Int.MAX_VALUE

        for (wire in wires) {

            // 간선 하나 제거
            val tempWires = wires.toMutableList() - wire

            val graph = mutableMapOf<Int, MutableSet<Int>>()
            tempWires.forEach {
                graph[it[0]] = graph.getOrDefault(it[0], mutableSetOf()).apply { add(it[1]) }
                graph[it[1]] = graph.getOrDefault(it[1], mutableSetOf()).apply { add(it[0]) }
            }

            // dfs로 가서 방문한 것 도출
            val visited = MutableList(n+1) {false}
            dfs(graph, visited, 1)
            val visitCount = visited.count { it }
            
            answer = min(answer, ((n - visitCount) - visitCount).absoluteValue)
        }

        return answer
    }

    private fun dfs(graph: MutableMap<Int, MutableSet<Int>>, visited: MutableList<Boolean>, position: Int) {
        if (visited[position]) {
            return
        }

        visited[position] = true

        for (newPosition in graph[position] ?: emptySet()) {
            dfs(graph, visited, newPosition)
        }
    }
}
```
