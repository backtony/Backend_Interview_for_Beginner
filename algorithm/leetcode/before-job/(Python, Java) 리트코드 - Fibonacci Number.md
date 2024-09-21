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

## kotlin 풀이
```kotlin
class Solution {
    fun fib(n: Int): Int {
        if (n == 0) return 0
        if (n == 1) return 1

        val fib = MutableList(n+1) {0}
        fib[1] = 1

        for (i in 2..n) {
            fib[i] = fib[i-1] + fib[i-2]
        }

        return fib[n]
    }
}
```
