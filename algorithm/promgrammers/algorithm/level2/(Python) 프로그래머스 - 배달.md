[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12978)


## 풀이
```python
import heapq


def solution(N, road, K):
    graph = [[] for _ in range(N + 1)]
    for x, y, cost in road:
        graph[x].append((cost, y))
        graph[y].append((cost, x))

    distance = dijkstra(graph, N)

    return len([x for x in distance if x <= K])


def dijkstra(graph, N):
    INF = int(1e9)
    q = []
    distance = [INF] * (N + 1)
    distance[1] = 0

    heapq.heappush(q, (0, 1))

    while q:
        cost1, pos1 = heapq.heappop(q)
        if distance[pos1] < cost1:
            continue
        for cost2, pos2 in graph[pos1]:
            if distance[pos2] > cost2 + cost1:
                distance[pos2] = cost2 + cost1
                heapq.heappush(q, (distance[pos2], pos2))

    return distance
```

## kotlin 풀이
```kotlin
import java.util.*

class Solution {
    fun solution(N: Int, road: Array<IntArray>, k: Int): Int {

        // a to (b, cost)
        val graph = mutableMapOf<Int, MutableList<Node>>()
        road.forEach {
            graph[it[0]] = graph.getOrDefault(it[0], mutableListOf()).apply { add(Node(it[1], it[2])) }
            graph[it[1]] = graph.getOrDefault(it[1], mutableListOf()).apply { add(Node(it[0], it[2])) }
        }

        // distance
        val distance = IntArray(N + 1) { Int.MAX_VALUE }
        distance[1] = 0
        
        // dijkstra 
        val queue = PriorityQueue<Node>(
            compareBy { it.cost }
        )

        queue.add(Node(1, 0))

        while (queue.isNotEmpty()) {
            val node = queue.poll()
            if (distance[node.id] < node.cost) {
                continue
            }

            for (newNode in graph.getOrDefault(node.id, mutableListOf())) {
                val newDistance = node.cost + newNode.cost
                if (distance[newNode.id] > newDistance) {
                    distance[newNode.id] = newDistance
                    queue.add(Node(newNode.id, newDistance))
                }
            }
        }

        return distance.count {
            it <= k
        }
    }

    class Node(
        val id: Int,
        val cost: Int,
    )
}
```




