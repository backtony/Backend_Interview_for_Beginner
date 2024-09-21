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

## kotlin 풀이
```kotlin
class Solution {
    fun productExceptSelf(nums: IntArray): IntArray {

        val leftTimes = MutableList(nums.size) { 1 }
        val rightTimes = MutableList(nums.size) { 1 }

        for (idx in nums.indices) {
            if (idx == 0) {
                leftTimes[idx] *= nums[idx]
                rightTimes[nums.lastIndex - idx] *= nums[nums.lastIndex - idx]
                continue
            }

            leftTimes[idx] = leftTimes[idx-1] * nums[idx]
            rightTimes[nums.lastIndex - idx] = nums[nums.lastIndex - idx] * rightTimes[nums.lastIndex - idx + 1]
        }

        val answer = MutableList(nums.size) { 0 }
        for (idx in answer.indices) {
            if (idx == 0) {
                answer[idx] = rightTimes[idx+1]
                continue
            }

            if (idx == answer.lastIndex) {
                answer[idx] = leftTimes[idx-1]
                continue
            }

            answer[idx] = leftTimes[idx-1] * rightTimes[idx+1]
        }
        return answer.toIntArray()
    }
}
```
