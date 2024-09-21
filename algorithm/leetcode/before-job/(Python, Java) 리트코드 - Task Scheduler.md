[문제 링크](https://leetcode.com/problems/task-scheduler/)


## Python 풀이
```python
from typing import List

from collections import Counter


class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        scheduler = sorted(Counter(tasks).items(), key=lambda x: x[1])
        max_frequency = scheduler.pop()[1]

        # 가장 개수가 많은 문자만 일렬로 나열했을 때 중간에 비어있는 유휴 시간
        idle_time = (max_frequency - 1) * n

        # 유휴 시간 채워주기
        while scheduler:
            idle_time -= min(scheduler.pop()[1], max_frequency - 1)

        # 유휴 시간이 음수가 되면 유휴 시간 없이 그냥 나열해도 수행가능해진다.
        idle_time = max(idle_time, 0)
        return len(tasks) + idle_time

```

## Java 풀이
```java
import java.util.HashMap;
import java.util.List;
import java.util.Map;
import java.util.stream.Collectors;

class Solution {
    public int leastInterval(char[] tasks, int n) {
        Map<Character, Integer> counter = new HashMap<>();

        for (char letter : tasks) {
            Integer cnt = counter.getOrDefault(letter, 0);
            counter.put(letter, cnt + 1);
        }

        List<Integer> count = counter.entrySet().parallelStream()
                .map(Map.Entry::getValue)
                .sorted()
                .collect(Collectors.toList());

        int size = counter.size();
        Integer maxCount = count.get(size - 1);
        int idleTime = (maxCount - 1) * n;

        for (int idx = size - 2; idx >= 0; idx--) {
            idleTime -= Math.min(count.get(idx),maxCount-1);
        }

        idleTime = Math.max(idleTime, 0);

        return tasks.length + idleTime;
    }
}
```

## kotlin 풀이
```kotlin
import kotlin.math.absoluteValue
import kotlin.math.min

class Solution {
    fun leastInterval(tasks: CharArray, n: Int): Int {

        val counter = mutableMapOf<Char, Int>()
        for (task in tasks) {
            counter[task] = counter.getOrDefault(task, 0) + 1
        }

        // 제일 많은 것을 기준으로 유휴시간을 계산
        val max = counter.maxBy { it.value }
        var idleTime = (max.value - 1).times(n)

        // tasks를 그대로 수행해도 될지, 사이에 추가 유휴시간이 필요할지 계산
        for (entry in counter) {

            if (entry.key == max.key) {
                continue
            }

            // 개수가 max.value랑 같은 경우라면 한개 적게 처리해서 유효시간 계산
            idleTime -= min(entry.value, max.value - 1)
        }

        // 유휴시간이 필요한 경우
        if (idleTime > 0) {
            return tasks.size + idleTime.absoluteValue
        }

        return tasks.size
    }
}
```
