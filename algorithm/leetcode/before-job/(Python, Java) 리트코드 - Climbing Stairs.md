[문제 링크](https://leetcode.com/problems/climbing-stairs/)


## Python 풀이
```python
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1:
            return 1
        if n == 2:
            return 2

        stairs = [0, 1, 2]

        for idx in range(3, n + 1):
            stairs.append(stairs[idx - 1] + stairs[idx - 2])

        return stairs[n]
```

## Java 풀이
```java
class Solution {
    public int climbStairs(int n) {
        int[] stairs = new int[n + 1];
        if (n == 1)
            return 1;
        if (n == 2)
            return 2;

        stairs[1] = 1;
        stairs[2] = 2;

        for (int idx = 3; idx <= n; idx++) {
            stairs[idx] = stairs[idx - 1] + stairs[idx - 2];
        }
        return stairs[n];
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun climbStairs(n: Int): Int {
        val accumulatedCount = MutableList(n+1) {1}
        if (n == 1) {
            return 1
        }

        var idx = 1

        while(idx != n) {
            idx++
            accumulatedCount[idx] = accumulatedCount[idx-1] + accumulatedCount[idx-2]
        }

        return accumulatedCount[n]
    }
}
```
