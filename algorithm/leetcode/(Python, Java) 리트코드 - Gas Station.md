[문제 링크](https://leetcode.com/problems/gas-station/)


## Python 풀이
```python
from typing import List


class Solution:
    def canCompleteCircuit(self, gas: List[int], cost: List[int]) -> int:

        if sum(gas) < sum(cost):
            return -1

        start = remain = 0
        for idx in range(len(gas)):
            if remain + gas[idx] < cost[idx]:
                start = idx + 1
                remain = 0
            else:
                remain += gas[idx] - cost[idx]

        return start
```

## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        // 합계가 더 적으면 가능성 없음
        if (Arrays.stream(gas).sum() < Arrays.stream(cost).sum())
            return -1;

        // 반드시 출발점이 존재하는 영역
        int start = 0;
        int remain = 0;
        int length = gas.length;        
        for (int idx = 0; idx < length; idx++) {
            // 성립되지 않는 지점이 있다면 그 앞은 전부 출발점이 될 수 없다.
            if (gas[idx] + remain < cost[idx]) {
                start = idx + 1;
                remain = 0;
            } else {
                remain += gas[idx] - cost[idx];
            }
        }
        return start;
    }
}
```
