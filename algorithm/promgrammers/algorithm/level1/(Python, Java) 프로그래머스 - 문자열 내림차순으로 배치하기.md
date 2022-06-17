[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12917)


## Python 풀이
```python
def solution(s):
    return "".join(sorted(s,reverse=True))
```

## Java 풀이
```java
class Solution {
    public String solution(String s) {
        char[] charArray = s.toCharArray();
        Arrays.sort(charArray);
        return new StringBuilder(String.valueOf(charArray)).reverse().toString();
    }
}
```
```java
// stream 풀이 -> 시간이 오래 걸린다.
import java.util.Collections;

class Solution {
    public String solution(String s) {
        return Stream.of(s.split("")).sorted(Collections.reverseOrder()).collect(Collectors.joining());
    }
}
```