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

## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun rob(nums: IntArray): Int {
        if (nums.size == 1) return nums[0]
        if (nums.size == 2) return nums.max()

        val accumulated = MutableList(nums.size) {0}
        accumulated[0] = nums[0]
        accumulated[1] = max(nums[1], nums[0])

        for (idx in 2..nums.lastIndex) {
            accumulated[idx] = max(accumulated[idx-1], accumulated[idx-2] + nums[idx])
        }

        return accumulated.last()
    }
}
```
