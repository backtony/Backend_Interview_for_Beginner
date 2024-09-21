[문제 링크](https://leetcode.com/problems/3sum/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun threeSum(nums: IntArray): List<List<Int>> {

        val sortedNums = nums.sorted()
        val answer = mutableListOf<List<Int>>()
        
        // 한개는 고정으로 쭉 진행하고 두번째 세번째 인덱스를 구한다.
        for (firstIdx in 0..nums.lastIndex - 2) {
            
            // 중복 제거
            if (firstIdx > 0 && sortedNums[firstIdx - 1] == sortedNums[firstIdx]) {
                continue
            }

            var left = firstIdx + 1
            var right = sortedNums.lastIndex

            while (left < right) {
                val sum = sortedNums[firstIdx] + sortedNums[left] + sortedNums[right]

                if (sum == 0) {
                    answer.add(listOf(sortedNums[firstIdx], sortedNums[left], sortedNums[right]))
                    left++
                    right--
                
                    // 중복 제거
                    while (left < right && sortedNums[left] == sortedNums[left - 1]) {
                        left++
                    }

                    while (left < right && sortedNums[right] == sortedNums[right + 1]) {
                        right--
                    }
                } else if (sum > 0) {
                    right--
                } else {
                    left++
                }
            }
        }

        return answer
    }
}
```
