[문제 링크](https://leetcode.com/problems/two-sum/)


## Python 풀이
```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        nums_map = dict()
        for idx, num in enumerate(nums):
            nums_map[num] = idx

        for idx, num in enumerate(nums):
            key = target - num

            value = nums_map.get(key)
            if value is not None and value != idx:
                return [value, idx]
```

## Java 풀이
```java
import java.util.HashMap;

class Solution {
    public int[] twoSum(int[] nums, int target) {
        // 초기화
        HashMap<Integer, Integer> numMap = new HashMap();
        for (int idx = 0; idx < nums.length; idx++) {
            numMap.put(nums[idx], idx);
        }

        int[] answer = new int[2];
        for (int idx = 0; idx < nums.length; idx++) {
            int remain = target - nums[idx];
            if (numMap.containsKey(remain) && numMap.get(remain) != idx) {
                answer[0] = idx;
                answer[1] = numMap.get(remain);
                break;
            }
        }
        return answer;
    }
}
```