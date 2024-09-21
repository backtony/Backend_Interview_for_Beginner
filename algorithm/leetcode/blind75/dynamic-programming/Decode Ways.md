[문제 링크](https://leetcode.com/problems/decode-ways/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun numDecodings(s: String): Int {

        val memo = MutableList(s.length) { 0 }
        val code = (1..26).map { it.toString() }

        for (idx in 0..s.lastIndex) {

            if (s.slice(0..idx) in code) {
                memo[idx] += 1
            }

            for (prev in 0 until idx) {
                val nextCode = s.slice(prev + 1..idx)
                if (memo[prev] != 0 && nextCode in code) {
                    memo[idx] += memo[prev]
                }
            }
        }

        return memo.last()
    }
}

```
