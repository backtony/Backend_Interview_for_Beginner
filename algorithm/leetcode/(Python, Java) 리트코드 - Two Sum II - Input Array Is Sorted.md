[문제 링크](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)


## Python 풀이
```python
from typing import List
from bisect import bisect_left

class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:

        length = len(numbers)
        for idx, number in enumerate(numbers, start=1):
            remain = target - number
            pair_idx = bisect_left(numbers, remain, idx)

            if pair_idx < length and numbers[pair_idx] == remain:
                return [idx, pair_idx + 1]
```
이진 탐색으로 풀었다.

## Java 풀이
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] twoSum(int[] numbers, int target) {
        Map<Integer, Integer> idxMap = new HashMap<>();

        int length = numbers.length;
        for (int idx = 0; idx < length; idx++) {
            idxMap.put(numbers[idx], idx + 1);
        }

        int[] answer = new int[2];
        for (int idx = 0; idx < length; idx++) {
            int remain = target - numbers[idx];
            if (idxMap.containsKey(remain)) {
                answer[0] = idx+1;
                answer[1] = idxMap.get(remain);
                break;
            }
        }
        return answer;

    }
}
```
map을 사용해서도 풀 수 있다.