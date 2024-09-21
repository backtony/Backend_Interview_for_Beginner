[문제 링크](https://leetcode.com/problems/climbing-stairs/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun climbStairs(n: Int): Int {
        val memo = MutableList(n){0}

        for (idx in 0 until n) {
            if (idx == 0) {
                memo[idx] = 1
                continue
            }

            if (idx == 1) {
                memo[idx] = 2
                continue
            }

            memo[idx] = memo[idx-1] + memo[idx-2]
        }

        return memo[n-1]
    }
}
```
