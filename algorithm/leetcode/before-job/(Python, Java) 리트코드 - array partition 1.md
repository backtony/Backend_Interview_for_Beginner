[문제 링크](https://leetcode.com/problems/array-partition-i/)


## Python 풀이
```python
from typing import List

class Solution:
    def arrayPairSum(self, nums: List[int]) -> int:
        return sum(sorted(nums)[::2])

if __name__ == '__main__':
    print(Solution().arrayPairSum([6, 2, 6, 5, 1, 2]))
```

## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);
        int answer = 0;
        for(int idx=0; idx<nums.length;idx+=2){
            answer += nums[idx];
        }
        return answer;
    }
}
```