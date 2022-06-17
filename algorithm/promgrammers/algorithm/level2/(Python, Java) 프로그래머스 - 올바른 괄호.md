[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12909)


## Python 풀이
```python
def solution(s):
    left_cnt = 0
    right_cnt = 0

    for letter in s:

        if letter == '(':
            left_cnt += 1
        else:
            right_cnt += 1

        if right_cnt > left_cnt:
            return False

    return left_cnt == right_cnt
```

## Java 풀이
```java
class Solution {
    boolean solution(String s) {
        int leftCnt = 0;
        int rightCnt = 0;

        for (char letter : s.toCharArray()) {
            if (letter == '(')
                leftCnt++;
            else
                rightCnt++;

            if (leftCnt < rightCnt)
                return false;
        }

        return leftCnt == rightCnt;
    }
}
```