[문제 링크](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun search(nums: IntArray, target: Int): Int {
        // 시작지점 찾기
        var left = 0
        var right = nums.lastIndex
        while(left <= right) {
            val mid = (left + right) / 2

            // mid가 시작점 일 수도 있고, 조금 더 클 수도 있다.
            if (nums[mid] < nums[right]) {
                right = mid
            } else {
                left = mid + 1
            }
        }

        // binarySearch는 정렬된 리스트에서 수행가능하므로 from, to 를 지정
        val leftIdx = nums.binarySearch(target, 0, right)
        val rightIdx = nums.binarySearch(target, right, nums.size)

        if (leftIdx >= 0) {
            return leftIdx
        }

        if (rightIdx >= 0) {
            return rightIdx
        }

        return -1
    }
}
```
