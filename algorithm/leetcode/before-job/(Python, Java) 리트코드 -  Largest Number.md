[문제 링크](https://leetcode.com/problems/largest-number/)


## Python 풀이
```python
import functools
from typing import List


class Solution:
    def largestNumber(self, nums: List[int]) -> str:
        def comparator(x, y):
            # 숫자 음수, 0, 양수 중 반환해야하므로 int로 변환시켜서 연산해야 한다.
            return int(x + y) - int(y + x)

        answer = ''.join(sorted(map(str, nums), key=functools.cmp_to_key(comparator), reverse=True))
        if answer[0] == '0':
            return '0'
        return answer
```

## Java 풀이
```java
import java.util.*;
import java.util.stream.Collectors;


class Solution {
    public String largestNumber(int[] nums) {
        int length = nums.length;
        String[] numStr = new String[length];
        for (int idx=0;idx<length;idx++){
            numStr[idx] = String.valueOf(nums[idx]);
        }

        Arrays.sort(numStr, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return (o2 + o1).compareTo(o1 + o2);
            }
        });

        String result = Arrays.stream(numStr).collect(Collectors.joining());
        if (result.charAt(0) == '0')
            return "0";
        return result;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun largestNumber(nums: IntArray): String {

        val result = nums.map { it.toString() }
            .sortedWith(
                Comparator { o1, o2 -> (o2 + o1).compareTo((o1 + o2)) }
            )
            .joinToString("")
        
        if (result[0] == '0') {
            return "0"
        }
        
        return result
    }
}
```
