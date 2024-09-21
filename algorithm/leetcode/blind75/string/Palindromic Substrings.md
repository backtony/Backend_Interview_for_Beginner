[문제 링크](https://leetcode.com/problems/palindromic-substrings/description/)


## kotlin 풀이
```kotlin
class Solution {

    fun countSubstrings(s: String): Int {
        var answer = 0
        for (start in 0..s.lastIndex) {

            answer += palindromeCount(s, start)
        }

        return answer
    }

    fun palindromeCount(s:String, start: Int): Int {

        var count = 0
        // 출발점을 기준으로 뒤쪽으로만 이동해서 palindrome인 경우 count 추가
        for (end in start..s.lastIndex) {
            val slice = s.slice(start..end)
            if (slice == slice.reversed()) {
                count++
            }
        }

        return count
    }
}
```
