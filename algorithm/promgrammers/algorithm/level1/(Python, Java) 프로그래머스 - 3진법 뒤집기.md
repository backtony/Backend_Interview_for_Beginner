[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/68935)


## PYthon 풀이1
```python
from collections import deque


def solution(n):
    answer = 0
    multi = 1

    q = deque()

    while n > 0:
        q.appendleft(n % 3)
        n //= 3

    for idx in range(len(q)):
        answer += q[idx] * multi
        multi *= 3

    return answer
```


## Python 풀이2
```python
def solution(n):
    answer = ""

    while n > 0:
        answer += str(n % 3)
        n //= 3

    return int(answer, 3)
```
int의 인자로 숫자와 표현된 진법을 전달하면 10진수로 반환해준다.

## Java 풀이
```java
class Solution {
    public int solution(int n) {
        StringBuilder sb = new StringBuilder();
        while (n >= 3) {
            sb.append(n % 3);
            n /= 3;
        }
        sb.append(n);

        return Integer.parseInt(sb.toString(), 3);
    }
}
```