[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12939)


## Python 풀이
```python
def solution(s):
    split = list(map(int, s.split()))
    return str(min(split)) + " " + str(max(split))
```

## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public String solution(String s) {
        int[] arr = Arrays.stream(s.split(" ")).mapToInt(Integer::parseInt).toArray();
        int max = Arrays.stream(arr).max().getAsInt();
        int min = Arrays.stream(arr).min().getAsInt();

        return min + " " +max;
    }
}
```