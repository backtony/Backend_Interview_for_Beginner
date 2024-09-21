[문제 링크](https://leetcode.com/problems/contains-duplicate/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun containsDuplicate(nums: IntArray): Boolean {
        return nums.size != nums.distinct().size
    }
}
```
