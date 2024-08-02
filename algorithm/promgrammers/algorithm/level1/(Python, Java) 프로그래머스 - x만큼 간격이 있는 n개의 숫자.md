[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12954)


## 풀이
```python
def solution(x, n):
    return [x + x * multi for multi in range(n)]
```

## Java 풀이
```java
class Solution {
    public long[] solution(int x, int n) {
        long[] answer = new long[n];
        long num = x;
        for (int idx = 0; idx < n; idx++) {
            answer[idx] = num;
            num += x;
        }
        return answer;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(x: Int, n: Int): LongArray {
        var result = mutableListOf<Long>()
        var num = x.toLong()
        for (i in 0 until n) {
            result.add(num)
            num += x
        }

        return result.toLongArray()
    }
}
```
