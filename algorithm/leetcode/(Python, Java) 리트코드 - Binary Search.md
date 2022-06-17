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
