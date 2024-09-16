[문제 링크](https://leetcode.com/problems/top-k-frequent-elements/)


## Python 풀이
```python
from collections import Counter
from typing import List


class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        counter = Counter(nums)
        answer = []
        for key, _ in counter.most_common(k):
            answer.append(key)
        return answer
```

## Java 풀이
```java
import java.util.Collections;
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] topKFrequent(int[] nums, int k) {

        Map<Integer, Integer> counter = new HashMap<>();
        for (int num : nums) {
            counter.put(num, counter.getOrDefault(num, 0) + 1);
        }

        return counter.entrySet().stream().sorted(Map.Entry.comparingByValue(Collections.reverseOrder()))
                .map(Map.Entry::getKey)
                .limit(k)
                .mapToInt(Integer::intValue)
                .toArray();
    }

}
```
comparingByValue() 다음에 .reversed가 자동완성으로 나오는데 사용할 수 없고 인자로 reverseOrder를 줘야 한다.


## kotlin 풀이
```kotlin
class Solution {
    fun topKFrequent(nums: IntArray, k: Int): IntArray {

        val counter = mutableMapOf<Int, Int>()
        for (num in nums) {
            counter[num] = counter.getOrDefault(num, 0) + 1
        }

        return counter.entries.sortedByDescending { it.value }
            .take(k)
            .map { it.key }
            .toIntArray()
    }
}
```
