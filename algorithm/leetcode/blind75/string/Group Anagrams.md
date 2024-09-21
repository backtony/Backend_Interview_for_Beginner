[문제 링크](https://leetcode.com/problems/group-anagrams/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun groupAnagrams(strs: Array<String>): List<List<String>> {
        
        val group = mutableMapOf<String, MutableList<String>>()

        for (str in strs) {
            val key = str.toCharArray().sorted().joinToString("")
            group[key] = group.getOrDefault(key, mutableListOf()).apply { add(str) }
        }
        
        return group.values.toList()
    }
}
```
