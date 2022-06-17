[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17680)


## Python 풀이
```python
from collections import deque


def solution(cacheSize, cities):
    if cacheSize == 0:
        return len(cities) * 5

    store = set()
    q = deque()
    time = 0
    for city in cities:
        city = city.lower()
        if city in store:
            time += 1
            q.remove(city)
            q.append(city)
        else:
            if len(q) == cacheSize:
                drop_city = q.popleft()
                store.remove(drop_city)

            q.append(city)
            store.add(city)
            time += 5

    return time
```
사실 큐만 사용하면 더 간결한 코드를 짤 수 있다.  
하지만 검색해서 지워야하는 로직 때문에 set을 사용해서 시간을 조금 더 줄였다.

## Java 풀이
```java
import java.util.HashSet;
import java.util.LinkedList;
import java.util.Queue;
import java.util.Set;

class Solution {
    public int solution(int cacheSize, String[] cities) {

        if (cacheSize == 0)
            return cities.length * 5;

        int time = 0;
        Queue<String> q = new LinkedList<>();
        Set<String> cache = new HashSet<>();
        for (String city : cities) {
            city = city.toLowerCase();
            if (cache.contains(city)) {
                time += 1;
                q.remove(city);
                q.add(city);
            } else {
                if (q.size() == cacheSize) {
                    String drop = q.poll();
                    cache.remove(drop);
                }
                q.add(city);
                cache.add(city);
                time += 5;
            }
        }
        return time;
    }
}
```