[문제 링크](https://leetcode.com/problems/top-k-frequent-elements/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun topKFrequent(nums: IntArray, k: Int): IntArray {
        val counter = mutableMapOf<Int,Int>()

        for (num in nums) {
            counter[num] = counter.getOrDefault(num,0)+1
        }

        return counter.entries.sortedByDescending { it.value }
            .take(k)
            .map { it.key }
            .toIntArray()
    }
}
```
