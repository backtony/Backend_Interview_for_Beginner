[문제 링크](https://leetcode.com/problems/product-of-array-except-self/)


## Python 풀이
```python
from typing import List


class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        answer = []
        # 왼쪽 곱
        temp = 1
        for num in nums:
            answer.append(temp)
            temp *= num

        # 오른쪽 곱
        temp = 1
        for idx in range(len(answer) - 1, -1, -1):
            answer[idx] *= temp
            temp *= nums[idx]

        return answer


if __name__ == '__main__':
    print(Solution().productExceptSelf([1, 2, 3, 4]))
```

## Java 풀이
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int length = nums.length;
        int[] answer = new int[length];

        // 왼쪽부터
        int temp = 1;
        for (int idx = 0; idx < length; idx++) {
            answer[idx] = temp;
            temp *= nums[idx];
        }

        temp = 1;
        for (int idx = length - 1; idx >= 0; idx--) {
            answer[idx] *= temp;
            temp *= nums[idx];
        }
        
        return answer;
    }
}
```