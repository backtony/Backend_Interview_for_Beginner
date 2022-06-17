[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12911)


## Python 풀이
```python
from collections import Counter


def solution(n):
    cnt = Counter(bin(n)[2:]).get('1')

    while True:
        n += 1
        temp = Counter(bin(n)[2:]).get('1')
        if temp == cnt:
            return n
```

## Java 풀이
```java
class Solution {
    public int solution(int n) {
        int cnt = 0;
        for (char letter : Integer.toBinaryString(n).toCharArray()) {
            if (letter == '1')
                cnt += 1;
        }

        while (true) {
            int tempCnt = 0;
            n += 1;
            for (char letter : Integer.toBinaryString(n).toCharArray()) {
                if (letter == '1')
                    tempCnt += 1;
            }
            if (tempCnt == cnt)
                return n;
        }

    }
}
```