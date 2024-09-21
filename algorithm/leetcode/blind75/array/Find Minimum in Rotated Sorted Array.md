[문제 링크](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun findMin(nums: IntArray): Int {
        var left = 0
        var right = nums.lastIndex

        while(left <= right) {
            val mid = (left + right) / 2

            // target은 mid거나 mid 앞쪽에 존재함.
            if (nums[mid] < nums[right]) {
                right = mid
            } else {
                left = mid + 1
            }
        }

        return nums[right]
    }
}
```
