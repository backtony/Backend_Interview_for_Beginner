[문제 링크](https://leetcode.com/problems/maximum-product-subarray/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {

    fun maxProduct(nums: IntArray): Int {
        val minMemo = MutableList(nums.size) {0}
        val maxMemo = MutableList(nums.size) {0}
        var answer = nums[0]

        for (idx in 0..nums.lastIndex) {
            if (idx == 0) {
                minMemo[idx] = nums[idx]
                maxMemo[idx] = nums[idx]
                continue
            }

            val temp = listOf(maxMemo[idx - 1] * nums[idx], minMemo[idx - 1] * nums[idx], nums[idx])
            maxMemo[idx] = temp.max()
            minMemo[idx] = temp.min()
            answer = max(answer, maxMemo[idx])
        }

        return answer
    }
}

```
