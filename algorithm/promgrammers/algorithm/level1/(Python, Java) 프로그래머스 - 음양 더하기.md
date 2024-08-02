[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/76501)


## Python 풀이
```python
def solution(absolutes, signs):
    answer = 0
    for idx in range(len(absolutes)):
        if signs[idx] is True:
            answer += absolutes[idx]
        else:
            answer -= absolutes[idx]

    return answer
```

## Java 풀이
```java
class Solution {
    public int solution(int[] absolutes, boolean[] signs) {
        int answer = 0;

        for (int i = 0; i < absolutes.length; i++) {
            answer += absolutes[i] * (signs[i] ? 1 : -1);
        }
        return answer;
    }
}
```

## Kotlin 풀이
```kotlin
class Solution {
    fun solution(absolutes: IntArray, signs: BooleanArray): Int {
        var result = 0
        absolutes.zip(signs.toList()) { absolute, sign ->
            when (sign) {
                true -> result += absolute
                false -> result -= absolute
            }
        }
        
        return result
    }
}
```
