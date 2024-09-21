[문제 링크](https://leetcode.com/problems/longest-palindromic-substring/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun longestPalindrome(s: String): String {

        var answer = ""
        for (idx in 0..s.lastIndex) {
            val even = palindrome(s, idx, idx + 1)
            val odd = palindrome(s, idx, idx + 2)

            answer = listOf(answer, even, odd).maxBy { it.length }
        }

        return answer
    }

    private fun palindrome(s: String, left: Int, right: Int): String {
        var newLeft = left
        var newRight = right

        var answer = s[0].toString() // 예외 케이스
        while (0 <= newLeft && newRight < s.length) {
            if (s[newLeft] == s[newRight]) {
                answer = s.slice(newLeft..newRight)
                newLeft--
                newRight++
            } else {
                break
            }
        }

        return answer
    }
}
```
