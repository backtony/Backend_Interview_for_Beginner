[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12928?language=python3)


## Python 풀이 1
```python
def solution(n):
    return sum([x for x in range(1,n + 1) if n % x == 0])

print(solution(12))
```


## Python 풀이 2
```python
import math

def solution(n):
    answer = 0
    half = int(math.sqrt(n))
    for i in range(1, half + 1):
        if n % i == 0:
            answer += i
            answer += n // i

    if half ** 2 == n:
        answer -= half
    return answer
```
다소 길지만 복잡도 면에서는 훨씬 낫다.

## Java 풀이
```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        for (int i = 1; i <= (int) Math.sqrt(n); i++) {
            if (n % i == 0) {
                if (n / i == i) {
                    answer += i;
                } else {
                    answer += i + n / i;
                }
            }
        }
        return answer;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(n: Int): Int {
        val sqrt = Math.sqrt(n.toDouble()).toInt()
        var result = 0
        for (i in 1..sqrt) {
            if (i * i == n) {
                result += i
            } else if (n % i == 0) {
                result += i
                result += n / i
            }
        }
        return result
    }
}
```
