[문제 링크](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun lengthOfLongestSubstring(s: String): Int {

        var substring = ""
        var answer = 0

        for (right in 0..s.lastIndex) {
            while(s[right] in substring) {
                substring = substring.slice(1..substring.lastIndex)
            }
            substring += s[right]
            answer = max(answer, substring.length)
        }

        return answer
    }
}
```
