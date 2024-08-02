[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/86051)


## Python 풀이
```python
def solution(numbers):
    answer = 0
    numbers = set(numbers)
    for number in range(1, 10):
        if number not in numbers:
            answer += number
    return answer
```

## Java 풀이
```java
import java.util.Arrays;
import java.util.stream.IntStream;

class Solution {
    public int solution(int[] numbers) {
        return IntStream.rangeClosed(0, 9).filter(target 
        -> Arrays.stream(numbers).noneMatch(number -> number == target)).sum();
    }
}
```

## kotlin 풀이
```kotlin
import java.util.stream.IntStream

class Solution {
    fun solution(numbers: IntArray): Int {
        return IntStream.range(1,10).filter { numbers.contains(it).not() }.sum()
    }
}
```
