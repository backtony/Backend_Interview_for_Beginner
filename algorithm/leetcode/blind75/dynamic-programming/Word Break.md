[문제 링크]()


## kotlin 풀이
```kotlin
class Solution {
    fun wordBreak(s: String, wordDict: List<String>): Boolean {

        val memo = MutableList(s.length){ false }

        for (idx in 0..s.lastIndex) {
            
            if (s.slice(0..idx) in wordDict) {
                memo[idx] = true
            }

            for (prev in 0 until idx) {

                if (memo[prev] && s.slice(prev+1..idx) in wordDict) {
                    memo[idx] = true
                }
            }
        }

        return memo.last()
    }
}
```
