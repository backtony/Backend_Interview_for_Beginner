[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/76502)


## 풀이
```python
def solution(s):
    answer = 0
    left = ["{", "[", "("]
    right = ["}", "]", ")"]
    for _ in range(len(s)):
        stack = []
        check = 1
        for unit in s:
            if len(stack) == 0 and unit in right:
                check = 0
                break

            if unit in left:
                stack.append(unit)
            else:
                if right.index(unit) != left.index(stack.pop()):
                    check = 0
                    break

        if check and len(stack) == 0:
            answer += 1
        s = s[1:] + s[0]

    return answer
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(s: String): Int {
        if (s.length <= 1) {
            return 0
        }

        var answer = 0
        val brackets = mapOf(
            '(' to ')',
            '{' to '}',
            '[' to ']',
        )

        IntRange(0, s.lastIndex).forEach { move ->
            val letters = "${s.substring(move)}${s.substring(0, move)}"
            val stack = mutableListOf<Char>()

            letters.forEachIndexed { index, letter ->

                // 첫번째가 오른쪽인 경우
                if (letter in brackets.values) {
                    if (stack.isEmpty()) {
                        return@forEach
                    }

                    
                    val right = brackets.entries.find { it.value == letter }!!.key
                    // 닫히지 않는다면
                    if (right != stack.last()) {
                        return@forEach
                    } else {
                        // 닫힌다면
                        stack.removeLast()
                    }
                } else {
                    stack.add(letter)
                }
            }

            if (stack.isEmpty()) {
                answer += 1
            }
        }

        return answer
    }
}
```




