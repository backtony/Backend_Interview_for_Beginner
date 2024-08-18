[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42747)


## Python 풀이
```python
from bisect import bisect_left

def solution(citations):
    citations.sort()
    length = len(citations)
    left = 0
    right = length

    while left <= right:
        mid = (left + right) // 2
        target = length - bisect_left(citations, mid)

        if mid <= target:
            left = mid + 1
        elif mid > target:
            right = mid - 1

    return right
```

## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public int solution(int[] citations) {
        int length = citations.length;
        int start = 0;
        int end = length;
        Arrays.sort(citations);

        while (start <= end) {
            int mid = (end + start) / 2;
            
            // binarySearch는 못 찾으면 음수를 뱉으며 그걸 양수로 바꾸고 -1해주면 원래 들어가야 할 인덱스 위치다.
            int idx = Arrays.binarySearch(citations, mid);
            if (idx < 0) {
                idx = -idx - 1;
            }
            int target = length - idx;

            if (mid <= target) {
                start = mid + 1;
            } else {
                end = mid - 1;
            }
        }

        return end;
    }
}
```

## kotlin 풀이
```kotlin
import kotlin.math.min

class Solution {
        fun solution(citations: IntArray): Int {
            return citations.sortedDescending().mapIndexed {
                    idx, item -> min(idx + 1, item)
            }.maxOrNull()!!
        }
}
```



