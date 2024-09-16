[문제 링크](https://leetcode.com/problems/3sum/)


## 풀이
```python
from typing import List


class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        answer = []
        nums.sort()

        for i in range(len(nums) - 2):
            # 중복제거
            if i > 0 and nums[i] == nums[i - 1]:
                continue

            left, right = i + 1, len(nums) - 1

            while left < right:
                sum = nums[i] + nums[left] + nums[right]
                if sum < 0:
                    left += 1
                elif sum > 0:
                    right -= 1
                else:
                    answer.append([nums[i], nums[left], nums[right]])

                    while left < right and nums[left] == nums[left + 1]:
                        left += 1
                    while left < right and nums[right] == nums[right - 1]:
                        right -= 1

                    left += 1
                    right -= 1
        return answer

if __name__ == '__main__':
    print(Solution().threeSum([-1, 0, 1, 2, -1, -4]))
```
투 포인터 문제인데 투포인터 문제는 아직 익숙치 않아서 생각하기 조금 어렵다.

## Java 풀이
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        int length = nums.length;
        Arrays.sort(nums);

        List<List<Integer>> answer = new ArrayList<>();
        for (int idx = 0; idx < length - 2; idx++) {
            
            // 중복 제거
            if (0 < idx && nums[idx - 1] == nums[idx])
                continue;

            int left = idx + 1;
            int right = length - 1;

            while (left < right) {
                int sum = nums[idx] + nums[left] + nums[right];
                if (sum > 0) {
                    right--;
                } else if (sum < 0) {
                    left++;
                } else {
                    answer.add(List.of(nums[idx], nums[left], nums[right]));
                    // 중복 제거
                    while (left < right && nums[left] == nums[left + 1])
                        left++;
                    while (left < right && nums[right] == nums[right - 1])
                        right--;

                    right--;
                    left++;
                }
            }
        }
        return answer;
    }
}
```
3개를 구해야 하므로 정렬시키고 1개를 기준으로 잡고 2개는 투포인터로 진행한다.  
중복 처리하는 경우를 제거해줘야하는 것을 유의해야 한다.

## kotlin
```kotlin
class Solution {
    fun threeSum(nums: IntArray): List<List<Int>> {
        val answer = mutableListOf<List<Int>>()
        val sortedNums = nums.sorted()
        for (firstIdx in 0..sortedNums.lastIndex - 2) {
            var left = firstIdx + 1
            var right = sortedNums.lastIndex
            
            // 중복 제거
            if (firstIdx > 0 && sortedNums[firstIdx] == sortedNums[firstIdx - 1]) {
                continue
            }

            while (left < right) {
                val result = sortedNums[left] + sortedNums[right] + sortedNums[firstIdx]

                when {
                    result == 0 -> {
                        answer.add(listOf(sortedNums[firstIdx], sortedNums[left], sortedNums[right]))
                        left++
                        right--

                        while (left < right && sortedNums[left] == sortedNums[left - 1]) {
                            left++
                        }
                        while (left < right && sortedNums[right] == sortedNums[right + 1]) {
                            right--
                        }
                    }

                    result > 0 -> {
                        right--
                    }

                    result < 0 -> {
                        left++
                    }
                }


            }
        }
        return answer

    }
}
```
combination을 사용할 경우 시간 초과
