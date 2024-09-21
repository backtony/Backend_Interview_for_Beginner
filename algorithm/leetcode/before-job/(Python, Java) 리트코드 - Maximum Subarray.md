[문제 링크](https://leetcode.com/problems/maximum-subarray/)


## Python 풀이
```python
from typing import List


class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        for idx in range(1, len(nums)):
            nums[idx] += nums[idx - 1] if nums[idx - 1] >= 0 else 0

        return max(nums)
```

## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public int maxSubArray(int[] nums) {
        for (int idx = 1; idx < nums.length; idx++) {
            nums[idx] += nums[idx - 1] >= 0 ? nums[idx - 1] : 0;
        }
        return Arrays.stream(nums).max().getAsInt();
    }
}
```
메모이제이션 누적으로 풀 수 있다.  
이전 값이 음수라면 현재 인덱스부터 다시 누적하면 되므로 0을 더해주도록 한다.

## kotlin 풀이
```kotlin
class Solution {
    fun maxSubArray(nums: IntArray): Int {
        for ((index, num) in nums.withIndex()) {
            if (index == 0) {
                continue
            }

            if (nums[index - 1] >= 0) {
                nums[index] = nums[index - 1] + num
            }
        }

        return nums.max()
    }
}
```

