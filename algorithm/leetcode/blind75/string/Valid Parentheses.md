[문제 링크](https://leetcode.com/problems/valid-parentheses/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun isValid(s: String): Boolean {

        val parenthesesList = mutableListOf<Parentheses>()
        parenthesesList.add(Parentheses('(', ')'))
        parenthesesList.add(Parentheses('[', ']'))
        parenthesesList.add(Parentheses('{', '}'))

        val stack = mutableListOf<Char>()

        for (letter in s) {
            val target = parenthesesList.find { it.left == letter || it.right == letter }!!
            if (target.left == letter) {
                stack.add(letter)
            } else {
                if (stack.isEmpty() || stack.last() != target.left) {
                    return false
                } else {
                    stack.removeLast()
                }
            }
        }

        if (stack.isNotEmpty()) {
            return false
        }

        return true
    }

    data class Parentheses(
        val left: Char,
        val right: Char,
    )
}
```
