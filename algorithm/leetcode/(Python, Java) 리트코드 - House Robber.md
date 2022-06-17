[문제 링크](https://leetcode.com/problems/house-robber/)


## Python 풀이
```python
from typing import List


class Solution:
    def rob(self, nums: List[int]) -> int:

        length = len(nums)
        if length == 1:
            return nums[0]

        nums[1] = max(nums[0], nums[1])
        if length == 2:
            return nums[1]

        for idx in range(2, length):
            nums[idx] = max(nums[idx - 1], nums[idx - 2] + nums[idx])
            
        return nums[length - 1]
```

## Java 풀이
```java
class Solution {
    public int rob(int[] nums) {
        int length = nums.length;

        if (length == 1)
            return nums[0];

        nums[1] = Math.max(nums[0], nums[1]);
        if (length == 2)
            return nums[1];

        for (int idx = 2; idx < length; idx++) {
            nums[idx] = Math.max(nums[idx - 1], nums[idx - 2] + nums[idx]);
        }
        
        return nums[length - 1];
    }
}
```
