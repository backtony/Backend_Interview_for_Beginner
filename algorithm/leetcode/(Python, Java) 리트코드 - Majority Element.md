[문제 링크](https://leetcode.com/problems/majority-element/)


## Python 풀이
```python
from typing import List

from collections import Counter

class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        return Counter(nums).most_common(1)[0][0]


```

## Java 풀이
```java
import java.util.*;

class Solution {
    public int majorityElement(int[] nums) {
        Map<Integer, Integer> counter = new HashMap<>();
        for (int num : nums) {
            counter.put(num, counter.getOrDefault(num, 0) + 1);
        }
        return Collections.max(counter.entrySet(), Map.Entry.comparingByValue()).getKey();
    }
}
```
