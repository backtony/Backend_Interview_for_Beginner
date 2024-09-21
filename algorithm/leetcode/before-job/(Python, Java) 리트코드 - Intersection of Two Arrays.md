[문제 링크](https://leetcode.com/problems/intersection-of-two-arrays/)


## Python 풀이
```python
from typing import List


class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        return list(set(nums1) & set(nums2))
```

## Java 풀이
```java
import java.util.*;

class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        for (Integer num : nums1) {
            set.add(num);
        }

        Set<Integer> answer = new HashSet<>();
        for (int num : nums2) {
            if (set.contains(num))
                answer.add(num);
        }
        return answer.parallelStream().mapToInt(Integer::intValue).toArray();
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun intersection(nums1: IntArray, nums2: IntArray): IntArray {
        return nums1.intersect(nums2.toSet()).toIntArray()
    }
}
```
