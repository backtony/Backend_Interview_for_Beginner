[문제 링크](https://leetcode.com/problems/valid-parentheses/)


## Python 풀이
```python
class Solution:
    def isValid(self, s: str) -> bool:
        store = {"[": "]", "{": "}", "(": ")"}

        stack = []
        for letter in s:

            # 왼쪽
            if letter in store:
                stack.append(letter)

            # 오른쪽 인데 빈 경우
            elif len(stack) == 0:
                return False

            # 오른쪽인데 안 빈경우
            else:
                pop = stack.pop()
                if store.get(pop) != letter:
                    return False

        return len(stack) == 0
```

## Java 풀이
```java
import java.util.*;

class Solution {

    public boolean isValid(String s) {
        Map<Character, Character> brackets = new HashMap();
        brackets.put('[', ']');
        brackets.put('{', '}');
        brackets.put('(', ')');

        Stack<Character> stack = new Stack<>();
        for (char letter : s.toCharArray()) {
            if (brackets.containsKey(letter))
                stack.add(letter);
            else if (!stack.isEmpty() && brackets.get(stack.peek()) == letter)
                stack.pop();                
            else {
                return false;
            }
        }

        return stack.isEmpty();
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun isValid(s: String): Boolean {

        val parenthesesList = listOf(
            Parentheses('{', '}'),
            Parentheses('(', ')'),
            Parentheses('[', ']'),
        )

        val stack = mutableListOf<Char>()
        for (letter in s) {

            val parentheses = parenthesesList.find { it.left == letter || it.right == letter }!!

            val isLeft = parentheses.left == letter
            if (isLeft) {
                stack.add(letter)
                continue
            }

            if (stack.isEmpty() || stack.last() != parentheses.left) {
                return false
            }

            stack.removeLast()
        }

        return stack.isEmpty()
    }

    data class Parentheses(
        val left: Char,
        val right: Char,
    )
}
```
