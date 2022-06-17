[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12919)


## Python 풀이
```python
def solution(seoul):
    return "김서방은 {}에 있다".format(seoul.index("Kim"))
```

## Java 풀이
```java
class Solution {
    public String solution(String[] seoul) {
        int idx = Arrays.asList(seoul).indexOf("Kim");
        return new StringBuilder("김서방은 ")
                .append(idx)
                .append("에 있다").toString();
    }
}
```