[문제 링크](https://leetcode.com/problems/longest-increasing-subsequence/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun lengthOfLIS(nums: IntArray): Int {
        val memo = MutableList(nums.size) { 1 }

        for (idx in 1..nums.lastIndex) {

            for (prevIdx in 0 until idx) {
                if (nums[prevIdx] < nums[idx]) {
                    memo[idx] = max(memo[idx], memo[prevIdx] + 1)
                }
            }
        }

        return memo.max()
    }
}
```
