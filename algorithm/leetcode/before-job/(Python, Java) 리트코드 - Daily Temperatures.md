[문제 링크](https://leetcode.com/problems/daily-temperatures/)


## Python 풀이
```python
from typing import List


class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        answer = [0] * len(temperatures)
        stack = []
        for cur_idx, num in enumerate(temperatures):

            while stack and temperatures[stack[-1]] < num:
                idx = stack.pop()
                answer[idx] = cur_idx - idx

            stack.append(cur_idx)

        return answer

```

## Java 풀이
```java
import java.util.Stack;

class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int length = temperatures.length;
        int[] answer = new int[length];

        Stack<Integer> stack = new Stack<>();
        for (int curIdx = 0; curIdx < length; curIdx++) {

            while (!stack.isEmpty() && temperatures[stack.peek()] < temperatures[curIdx]) {
                Integer idx = stack.pop();
                answer[idx] = curIdx - idx;
            }
            stack.push(curIdx);
        }

        return answer;
    }

}
```

## kotlin 풀이
```kotlin
class Solution {
    fun dailyTemperatures(temperatures: IntArray): IntArray {

        val answer = MutableList(temperatures.size) {0}
        val q = mutableListOf<Pair<Int, Int>>()

        for ((idx, temperature) in temperatures.withIndex()) {
            if (q.isEmpty()) {
                q.add(Pair(idx, temperature))
                continue
            }

            while(q.isNotEmpty() && q.last().second < temperature) {
                val last = q.removeLast()
                answer[last.first] = idx - last.first
            }
            q.add(Pair(idx, temperature))
        }

        return answer.toIntArray()
    }
}
```
