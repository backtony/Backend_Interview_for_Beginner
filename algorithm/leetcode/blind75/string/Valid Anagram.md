[문제 링크](https://leetcode.com/problems/valid-anagram/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun isAnagram(s: String, t: String): Boolean {
        return s.toCharArray().sorted() == t.toCharArray().sorted()
    }
}
```
