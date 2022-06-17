[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12931)


## Python풀이
```python
def solution(n):
    return sum(list(map(int, str(n))))
```

## Java 풀이
```java
public class Solution {
    public int solution(int n) {
        int answer = 0;

        for (char ch : String.valueOf(n).toCharArray()) {
            answer += Character.getNumericValue(ch);
        }

        return answer;
    }
}
```