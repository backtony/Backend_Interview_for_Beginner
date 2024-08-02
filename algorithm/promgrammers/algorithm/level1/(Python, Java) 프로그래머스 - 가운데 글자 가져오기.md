[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12903)


## Python 풀이
```python
def solution(s):
    length = len(s)
    mid = length // 2

    return s[mid - 1:mid + 1] if length % 2 == 0 else s[mid]
```

## Java 풀이
```java
class Solution {
    public String solution(String s) {
        int length = s.length();
        int mid = length / 2;
        return length % 2 == 1 ? s.substring(mid, mid + 1) : s.substring(mid - 1, mid + 1);
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(s: String): String {
        val half = s.length / 2
        return when (isOdd(s.length)) {
            true -> { s[half].toString()}
            false -> { s.substring(half-1, half+1)}
        }
    }

    private fun isOdd(x: Int) = x % 2 != 0
}
```
