[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12933)


## Python 풀이
```python
def solution(n):
    answer = list(str(n))
    answer.sort(reverse=True)
    return int("".join(answer))
```


## Java 풀이
```java
class Solution {
    public long solution(long n) {
        String[] split = String.valueOf(n).split("");
        String collect = Stream.of(split).sorted(Collections.reverseOrder()).collect(Collectors.joining());
        return Long.parseLong(collect);
    }
}
```