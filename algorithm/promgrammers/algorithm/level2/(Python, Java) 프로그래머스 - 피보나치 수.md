[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12945?language=python3)


## Python 풀이
```python
def solution(n):
    dp=[0]*(n+1)
    dp[0]=0
    dp[1]=1       
    fibo(dp,n)
    return dp[n] % 1234567

def fibo(dp,n):
    for i in range(2,n+1):
        dp[i] = dp[i-1] + dp[i-2]
```

## Java 풀이
```java
class Solution {
    public int solution(int n) {
        if (n == 0)
            return 0;

        if (n == 1)
            return 1;

        int[] dp = new int[n + 1];
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i <= n; i++) {
            dp[i] = (dp[i - 2] + dp[i - 1])% 1234567;
        }

        return dp[n];
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(n: Int): Int {
        val table = MutableList(n + 1) { it }
        if (n <= 1) {
            return table[n]
        }

        for (idx in 2..n) {
            table[idx] = (table[idx - 2] + table[idx - 1]).mod(1234567)
        }

        return table[n]
    }
}
```
