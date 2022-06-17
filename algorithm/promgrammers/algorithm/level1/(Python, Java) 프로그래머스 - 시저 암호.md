[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12926)


## Python 풀이
```python
def solution(s, n):
    answer = ''
    for alpha in s:
        tmp = ord(alpha) + n
        if alpha.islower():
            answer += chr((tmp - ord('a')) % 26 + ord('a'))
        elif alpha.isupper():
            answer += chr((tmp - ord('A')) % 26 + ord('A'))
        else:
            answer += alpha

    return answer
```

## Java 풀이
```java
class Solution {
    public String solution(String s, int n) {
        StringBuilder sb = new StringBuilder();
        for (char ch : s.toCharArray()) {
            if (Character.isUpperCase(ch)) {
                sb.append((char) ('A' + (ch - 'A' + n) % 26));
            } else if (Character.isLowerCase(ch)) {
                sb.append((char) ('a' + (ch - 'a' + n) % 26));
            } else {
                sb.append(ch);
            }
        }
        return sb.toString();
    }
}
```