[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12934)


## Python 풀이
```python
import math

def solution(n):
    answer = -1
    half = int(math.sqrt(n))
    if half ** 2 == n:
        answer = (half + 1) ** 2

    return answer
```

## Java 풀이
```java
class Solution {
    public long solution(long n) {
        if (Math.pow((int)Math.sqrt(n),2) == n){
            return (long) Math.pow(Math.sqrt(n)+1,2);
        }
        return -1;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(n: Long): Long {
        val sqrt = Math.sqrt(n.toDouble())
        if (sqrt % 1.0 == 0.0) {
            return (sqrt + 1).pow(2).toLong()
        }
        return -1
    }
}
```
