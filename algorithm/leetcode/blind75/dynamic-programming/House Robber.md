[문제 링크](https://leetcode.com/problems/house-robber/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun rob(nums: IntArray): Int {
        if (nums.size == 1) return nums.first()

        val memo = MutableList(nums.size) { 0 }
        memo[0] = nums[0]

        for (idx in 1..nums.lastIndex) {
            if (idx == 1) {
                memo[idx] = max(nums[idx], nums[idx - 1])
                continue
            }

            memo[idx] = max(memo[idx - 2] + nums[idx], memo[idx - 1])
        }

        return memo.last()
    }
}
```
