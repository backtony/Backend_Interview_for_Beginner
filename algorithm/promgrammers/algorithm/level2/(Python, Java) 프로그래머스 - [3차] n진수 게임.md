[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17687)


## Python 풀이
```python
from collections import deque


def solution(n, t, m, p):
    table = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F']

    ls = []
    cnt = m * t
    num = 0
    while len(ls) <= cnt:
        temp = num
        q = deque()
        while temp >= n:
            remain = temp % n
            q.appendleft(table[remain])
            temp //= n

        q.appendleft(table[temp])
        ls.extend(q)
        num += 1

    answer = ""
    p -= 1
    while len(answer) != t:
        answer += ls[p]
        p += m
    
    return answer
```

## Java 풀이
```java
class Solution {
    public String solution(int n, int t, int m, int p) {
        char[] table = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F'};

        int cnt = m * t;
        int num = 0;
        List<Character> content = new ArrayList<>();
        while (content.size() < cnt) {
            int temp = num;
            LinkedList<Character> q = new LinkedList<>();
            while (temp >= n) {
                q.addFirst(table[temp % n]);
                temp /= n;
            }
            q.addFirst(table[temp]);
            content.addAll(q);
            num += 1;
        }

        p -= 1;
        StringBuilder sb = new StringBuilder();
        while (sb.length() != t) {
            sb.append(content.get(p));
            p += m;
        }

        return sb.toString();
    }

}
```