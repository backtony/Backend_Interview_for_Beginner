[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/70128)


## Python 풀이
```python
def solution(a, b):
    answer = 0
    for idx in range(len(a)):
        answer += a[idx] * b[idx]
    return answer
```

## Java 풀이
```java
class Solution {
    public int solution(int[] a, int[] b) {
        int answer = 0;
        for (int i = 0; i < a.length; i++) {
            answer += a[i] * b[i];
        }
        return answer;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(a: IntArray, b: IntArray): Int {
        return a.zip(b){ first, second ->
            second.times(first)
        }.sum()
    }
}
```
