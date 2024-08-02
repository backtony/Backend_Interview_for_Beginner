[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12918)


## Python 풀이
```python
def solution(s):    
    return s.isnumeric() and len(s) in [4,6]
```

## Java 풀이
```java
class Solution {
    public boolean solution(String s) {

        int length = s.length();
        if (length == 4 || length == 6)
            return s.matches("^[0-9]*$");
        return false;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(s: String): Boolean {

        if (s.length != 4 && s.length != 6) {
            return false
        }

        if (s.any { it.isDigit().not() }) {
            return false
        }

        return true
    }
}
```
