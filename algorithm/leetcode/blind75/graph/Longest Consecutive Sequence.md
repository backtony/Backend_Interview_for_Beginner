[문제 링크](https://leetcode.com/problems/longest-consecutive-sequence/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun longestConsecutive(nums: IntArray): Int {
        if (nums.isEmpty()) return 0

        var answer = 1
        val sortedNums = nums.sorted()
        val dp = MutableList(nums.size) { 1 }
        for (idx in 1..nums.lastIndex) {
            if (sortedNums[idx] == sortedNums[idx-1] + 1) {
                dp[idx] = dp[idx-1] + 1
                answer = max(answer, dp[idx])
            } else if (sortedNums[idx] == sortedNums[idx-1]) {
                dp[idx] = dp[idx-1]
            }
        }

        return answer
    }
}
```
