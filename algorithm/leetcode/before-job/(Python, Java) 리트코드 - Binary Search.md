[문제 링크](https://leetcode.com/problems/binary-search/)


## Python 풀이
```python
from typing import List
from bisect import bisect_left

class Solution:
    def search(self, nums: List[int], target: int) -> int:
        idx = bisect_left(nums, target)

        if idx >= len(nums) or nums[idx] != target:
            idx = -1

        return idx
```

## Java 풀이
```java
class Solution {
    public int search(int[] nums, int target) {
        int start = 0;
        int end = nums.length-1;

        while (start<=end){
            int mid = (start+end)/2;

            if (nums[mid]<target)
                start = mid+1;
            else if (nums[mid]> target)
                end = mid-1;
            else
                return mid;
        }
        return -1;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun search(nums: IntArray, target: Int): Int {

        var min = 0
        var max = nums.lastIndex

        while (min <= max) {
            val half = (min + max) / 2

            when {
                nums[half] == target -> return half
                nums[half] < target -> {
                    min = half + 1
                }

                else -> {
                    max = half - 1
                }
            }

        }

        return -1
    }
}
```
