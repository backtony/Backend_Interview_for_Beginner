[문제 링크](https://leetcode.com/problems/palindromic-substrings/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun countSubstrings(s: String): Int {

        var answer = 0
        for (idx in 0..s.lastIndex - 1) {

            val even = countPalindrome(s, idx, idx + 1)
            val odd = countPalindrome(s, idx, idx + 2)
            answer += even + odd
        }

        return answer + s.length
    }


    fun countPalindrome(s: String, left: Int, right: Int): Int {
        var count = 0
        var newLeft = left
        var newRight = right

        while (0 <= newLeft && newRight <= s.lastIndex && s[newLeft] == s[newRight]) {
            count++
            newLeft--
            newRight++
        }

        return count
    }
}
```
