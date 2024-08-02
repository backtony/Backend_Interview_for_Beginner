[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12912)


## Python 풀이
```python
def solution(a, b):
    return sum([x for x in range(min(a,b),max(a,b)+1)])
```
수학 공식을 쓰면 더 빠르겠지만, 그건 공식을 알아야만 풀 수 있으므로 사용하지 않았다.

## Java 풀이
```java
class Solution {
    public long solution(int a, int b) {
        long answer = 0;
        int small = Math.min(a, b);
        int big = Math.max(a, b);
        for (int i = small; i <= big; i++)
            answer += i;

        return answer;
    }
}
```

## kotlin 풀이
```kotlin
import kotlin.math.max
import kotlin.math.min

class Solution {
    fun solution(a: Int, b: Int): Long {
        if (a == b) return a.toLong()

        val min = min(a, b)
        val max = max(a,b)

        var result = 0.toLong()
        for (num in min .. max) {
            result += num
        }

        return result
    }
}
```
