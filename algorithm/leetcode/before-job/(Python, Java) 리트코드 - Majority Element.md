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

## kotlin 풀이
```kotlin
class Solution {
    fun majorityElement(nums: IntArray): Int {
        val counter = mutableMapOf<Int, Int>()

        nums.forEach {
            counter[it] = counter.getOrDefault(it, 0) + 1
        }

        return counter.entries.first { it.value > nums.size / 2 }.key
    }
}
```
