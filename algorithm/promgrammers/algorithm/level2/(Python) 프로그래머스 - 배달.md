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






