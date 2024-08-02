[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12944)


## Python 풀이
```python
def solution(arr):
    return sum(arr) / len(arr)
```

## Java 풀이
```java
class Solution {
    public double solution(int[] arr) {
        return Arrays.stream(arr).sum()/(double)arr.length;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(arr: IntArray): Double {
        return arr.average()
    }
}
```
