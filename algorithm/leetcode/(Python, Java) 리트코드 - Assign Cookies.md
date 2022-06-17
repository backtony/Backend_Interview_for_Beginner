[문제 링크](https://leetcode.com/problems/assign-cookies/)


## Python 풀이
```python
from typing import List

class Solution:
    def findContentChildren(self, g: List[int], s: List[int]) -> int:
        g.sort()  # 자식
        s.sort()  # 쿠기

        gIdx = sIdx = 0
        answer = 0
        while gIdx < len(g) and sIdx < len(s):
            if g[gIdx] <= s[sIdx]:
                gIdx += 1
                answer += 1

            sIdx += 1

        return answer
```

## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);
        int gIdx = 0; // 자식
        int sIdx = 0; // 쿠키
        int answer = 0;

        while (gIdx < g.length && sIdx < s.length) {
            if (g[gIdx] <= s[sIdx]) {
                gIdx++;
                answer++;
            }
            sIdx++;
        }
        return answer;
    }
}
```
