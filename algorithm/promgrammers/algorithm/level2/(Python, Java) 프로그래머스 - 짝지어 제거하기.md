[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12973)


## Python 풀이
```python
from collections import deque

def solution(s):
    answer = 1

    q = deque()
    for word in s:
        if not q:
            q.append(word)
        else:
            if q[-1] != word:
                q.append(word)
            else:
                q.pop()

    if q:
        answer = 0

    return answer
```
주어진 수 최대가 100만이다.  
이는 단순한 규칙 노가다로는 해결되지 않는 복잡도이다.  
이런 문제는 대부분이 자료구조를 사용해야하거나 특별하게 범위를 줄일 수 있느 규칙이 필요하다.



## Java 풀이
```java
import java.util.Stack;

class Solution {
    public int solution(String s) {
        Stack<Character> stack = new Stack<>();

        for (char ch : s.toCharArray()) {
            if (stack.isEmpty() || stack.peek() != ch) {
                stack.push(ch);
            } else if (stack.peek() == ch) {
                stack.pop();
            }
        }

        if (stack.isEmpty())
            return 1;
        return 0;
    }
}
```