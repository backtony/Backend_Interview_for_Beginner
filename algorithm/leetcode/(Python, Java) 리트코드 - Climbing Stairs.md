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
