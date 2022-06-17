[문제 링크](https://leetcode.com/problems/fibonacci-number/)


## Python 풀이
```python
class Solution:
    def fib(self, n: int) -> int:
        memo = [0] * (n + 1)

        if n >= 1:
            memo[1] = 1

        for idx in range(2, n + 1):
            memo[idx] = memo[idx - 1] + memo[idx - 2]

        return memo[n]
```

## Java 풀이
```java
class Solution {
    public int fib(int n) {
        int[] memo = new int[n + 1];

        if (n >= 1)
            memo[1] = 1;

        for (int idx = 2; idx <= n; idx++) {
            memo[idx] = memo[idx - 1] + memo[idx - 2];
        }
        return memo[n];
    }
}
```
