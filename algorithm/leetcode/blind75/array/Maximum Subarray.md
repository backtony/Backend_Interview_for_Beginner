[문제 링크](https://leetcode.com/problems/maximum-subarray/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun maxSubArray(nums: IntArray): Int {
        val memo = MutableList(nums.size) {0}
        var answer = nums[0]

        for (idx in 0..nums.lastIndex) {
            if (idx == 0) {
                memo[idx] = nums[idx]
                continue
            }

            memo[idx] = max(memo[idx-1] + nums[idx], nums[idx])
            answer = max(answer, memo[idx])
        }

        return answer
    }
}
```
