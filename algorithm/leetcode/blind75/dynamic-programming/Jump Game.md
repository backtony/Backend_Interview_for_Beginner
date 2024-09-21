[문제 링크](https://leetcode.com/problems/jump-game/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun canJump(nums: IntArray): Boolean {

        val dp = MutableList(nums.size) { false }
        dp[0] = true

        for (idx in 0..nums.lastIndex) {
            if (dp[idx].not()) {
                continue
            }

            for (move in 0..nums[idx]) {
                val next = idx + move
                if (next < nums.size) {
                    dp[next] = true
                }
            }
        }

        return dp.last()
    }
}
```
