[문제 링크](https://leetcode.com/problems/house-robber-ii/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    // 첫번째를 선택하는 경우 -> dp의 마지막을 없는 것으로 취급
    // 첫번째를 선택하지 않는 경우 => 2번째 부터 시작

    fun rob(nums: IntArray): Int {
        if (nums.size <= 2) return nums.max()

        val selectFirstHouseMemo = MutableList(nums.size-1) { 0 }
        selectFirstHouseMemo[0] = nums[0]
        selectFirstHouseMemo[1] = listOf(nums[0], nums[1]).max()

        for (idx in 2..nums.lastIndex-1) {
            selectFirstHouseMemo[idx] = max(selectFirstHouseMemo[idx - 2] + nums[idx], selectFirstHouseMemo[idx - 1])
        }

        val notSelectFirstHouseMemo = MutableList(nums.size) { 0 }
        notSelectFirstHouseMemo[0] = 0
        notSelectFirstHouseMemo[1] = nums[1]

        for (idx in 2..nums.lastIndex) {
            notSelectFirstHouseMemo[idx] = max(notSelectFirstHouseMemo[idx - 2] + nums[idx], notSelectFirstHouseMemo[idx - 1])
        }

        return max(notSelectFirstHouseMemo.max(), selectFirstHouseMemo.max())
    }
}

```
