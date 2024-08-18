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


## kotlin 풀이
```kotlin
class Solution {
    fun solution(p: String): String {
        if (p.isBlank()) {
            return ""
        }

        val balanceIndex = extractBalanceIndex(p)
        val u = p.substring(0, balanceIndex+1)
        val v = p.substring(balanceIndex+1)

        if (isCorrectLetters(u)) {
            return "$u${solution(v)}"
        } else {
            val reversed = u.substring(1, u.lastIndex).map {
                if (it == '(') {
                    ')'
                } else {
                    '('
                }
            }.joinToString("")

            return "(${solution(v)})$reversed"
        }
    }

    private fun extractBalanceIndex(p: String): Int {
        var left = 0
        var right = 0
        p.forEachIndexed { index, letter ->
            if (letter == '(') {
                left += 1
            } else {
                right += 1
            }

            if (left == right) {
                return index
            }
        }

        return -1
    }

    private fun isCorrectLetters(letters: String): Boolean {
        val stack = mutableListOf<Char>()

        letters.forEach {
            if (it == '(') {
                stack.add(it)
            } else {
                if (stack.isEmpty()) {
                    return false
                }

                stack.removeLast()
            }
        }

        return stack.isEmpty()
    }
}
```




