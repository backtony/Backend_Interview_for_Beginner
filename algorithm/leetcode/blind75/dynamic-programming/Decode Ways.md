[문제 링크](https://leetcode.com/problems/decode-ways/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun numDecodings(s: String): Int {
        if (s[0] =='0') return 0

        val dp = MutableList(s.length) { 0 }
        dp[0] = 1

        for (idx in 1..s.lastIndex) {
            val one = s[idx].toString().toInt()
            val two = s.slice(idx - 1..idx).toInt()

            if (two in 10..26) {
                if (idx-2 >=0) {
                    dp[idx] += dp[idx-2]
                } else {
                    dp[idx] = 1
                }
            }
            if (one in 1..9) {
                dp[idx] += dp[idx-1]
            }
        }

        return dp.last()
    }
}
```
