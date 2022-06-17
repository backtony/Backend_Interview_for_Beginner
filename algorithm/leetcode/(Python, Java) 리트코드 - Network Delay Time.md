[문제 링크](https://leetcode.com/problems/network-delay-time/)


## Python 풀이
```python
from typing import List
import heapq

class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        INF = int(1e9)

        def dijkstra():
            distance = [INF] * (n + 1)
            distance[k] = distance[0] = 0

            q = [(0, k)]

            while q:
                cost, now = heapq.heappop(q)

                if distance[now] < cost:
                    continue

                for next_cost, next in graph[now]:
                    if next_cost + cost < distance[next]:
                        distance[next] = next_cost + cost
                        heapq.heappush(q, (distance[next], next))

            return distance

        # 그래프 초기화
        graph = [[] for _ in range(n + 1)]
        for time in times:
            start, end, cost = time
            graph[start].append((cost, end))

        distance = dijkstra()
        answer = max(distance)
        if answer == INF:
            return -1
        return answer

```

## Java 풀이
```java
import java.util.*;

class Solution {
    private Map<Integer, List<Pair>> graph = new HashMap<>();

    public int networkDelayTime(int[][] times, int n, int k) {

        for (int[] time : times) {
            int start = time[0];
            int end = time[1];
            int cost = time[2];

            List<Pair> pairs = graph.getOrDefault(start, new ArrayList<Pair>());
            pairs.add(new Pair(end, cost));
            graph.put(start, pairs);
        }

        int[] distance = dijkstra(n, k);
        int max = Arrays.stream(distance).max().getAsInt();
        if (max == Integer.MAX_VALUE)
            return -1;
        return max;
    }

    private int[] dijkstra(int size, int start) {
        int[] distance = new int[size + 1];
        Arrays.fill(distance, Integer.MAX_VALUE);
        distance[start] = distance[0] = 0;

        PriorityQueue<Pair> pairs = new PriorityQueue<>();
        pairs.add(new Pair(start, 0));

        while (!pairs.isEmpty()) {

            Pair now = pairs.poll();
            if (distance[now.pos] < now.cost)
                continue;

            List<Pair> nextList = graph.getOrDefault(now.pos, new ArrayList<>());
            for (Pair next : nextList) {
                if (next.cost + now.cost < distance[next.pos]) {
                    distance[next.pos] = next.cost + now.cost;
                    pairs.add(new Pair(next.pos, distance[next.pos]));
                }
            }
        }
        return distance;
    }

    private class Pair implements Comparable<Pair> {
        int pos;
        int cost;

        public Pair(int pos, int cost) {
            this.pos = pos;
            this.cost = cost;
        }

        @Override
        public int compareTo(Pair o) {
            return Integer.compare(this.cost, o.cost);
        }
    }
}
```
