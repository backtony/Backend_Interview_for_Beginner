[문제 링크](https://leetcode.com/problems/two-sum/)


## kotlin 풀이
```kotlin
class Solution {
    fun twoSum(nums: IntArray, target: Int): IntArray {
        
        // 같은 수는 뒤쪽 인덱스로 덮어 씌운다.
        val accumulated = mutableMapOf<Int, Int>()
        nums.forEachIndexed { index, num ->
            accumulated[num] = index
        }

        nums.forEachIndexed { index, num ->
            val remain = target - num
            val remainIdx = accumulated[remain]

            if (remainIdx != null && remainIdx != index) {
                return intArrayOf(index, remainIdx)
            }
        }

        return intArrayOf(0,0)
    }
}
```
