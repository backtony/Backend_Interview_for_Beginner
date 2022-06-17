[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12937)


## Python 풀이
```python
def solution(num):
    return "Even" if num % 2 == 0 else "Odd"
```

## Java 풀이
```java
class Solution {
    public String solution(int num) {
        return num % 2 == 0 ? "Even" : "Odd";
    }   
}
```