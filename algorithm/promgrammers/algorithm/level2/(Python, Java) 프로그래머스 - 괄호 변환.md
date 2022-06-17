[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/60058)


## Python 풀이
```python
def solution(p):
    answer = ""
    length = len(p)
    if length == 0:
        return answer

    u, v = getUAndV(length, p)

    if isCorrectString(u):
        return u + solution(v)

    answer = "(" + solution(v) + ")" + ''.join([')' if x == '(' else '(' for x in u[1:-1]])
    return answer

def getUAndV(length, p):
    left = 0
    right = 0
    for idx in range(length):
        if p[idx] == '(':
            left += 1
        else:
            right += 1

        if left == right:
            break
    u = p[:idx + 1]
    v = p[idx + 1:]
    return u, v

def isCorrectString(u):
    left = 0
    right = 0
    key = 1
    for unit in u:
        if unit == '(':
            left += 1
        else:
            right += 1

        if right > left:
            key = 0
            break
    return key
```

## Java 풀이
```java
class Solution {
    public String solution(String p) {
        String answer = "";

        if (p.length() == 0)
            return answer;

        if (isCorrectString(p))
            return p;

        int left = 0, right = 0, idx = 0;

        char[] chars = p.toCharArray();
        for (; idx < p.length(); idx++) {
            if (chars[idx] == '(')
                left++;
            else
                right++;

            if (left == right)
                break;
        }

        String u = p.substring(0, idx + 1);
        String v = p.substring(idx + 1);

        if (isCorrectString(u)) {
            return u + solution(v);
        }
        
        StringBuilder sb = new StringBuilder().append("(").append(solution(v)).append(")");
        for (char ch : u.substring(1, u.length() - 1).toCharArray()) {
            if (ch == ')')
                sb.append('(');
            else
                sb.append(')');
        }
        return sb.toString();
    }

    private boolean isCorrectString(String u) {
        int left = 0;
        int right = 0;

        for (char ch : u.toCharArray()) {
            if (ch == '(')
                left++;
            else
                right++;
            if (left < right)
                return false;
        }
        return true;
    }
}
```





