[문제 링크](https://leetcode.com/problems/valid-palindrome/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun isPalindrome(s: String): Boolean {
        val replace = s.lowercase().replace("[^a-z0-9]+".toRegex(), "")
        return replace == replace.reversed()
    }
}
```
