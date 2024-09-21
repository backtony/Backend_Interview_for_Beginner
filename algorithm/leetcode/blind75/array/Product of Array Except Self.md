[문제 링크](https://leetcode.com/problems/product-of-array-except-self/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun productExceptSelf(nums: IntArray): IntArray {

        val left = MutableList(nums.size) { 1 }
        val right = MutableList(nums.size) { 1 }
        val answer = MutableList(nums.size) { 1 }
        
        // 왼쪽, 오른쪽 누적 곱
        for (idx in 0..nums.lastIndex) {
            if (idx == 0) {
                left[idx] = nums[idx]
                right[nums.lastIndex] = nums.last()
                continue
            }

            left[idx] = left[idx-1] * nums[idx]
            right[nums.lastIndex - idx] = right[nums.lastIndex - idx + 1] * nums[nums.lastIndex - idx]
        }
        
        // 계산
        for (idx in 0..nums.lastIndex) {
            if (idx == 0) {
                answer[idx] = right[idx+1]
                continue
            }
            if (idx == nums.lastIndex) {
                answer[idx] = left[nums.lastIndex-1]
                continue
            }
            answer[idx] = left[idx-1] * right[idx+1]
        }

        return answer.toIntArray()
    }
}
```
