[문제 링크](https://leetcode.com/problems/remove-duplicate-letters/)


## Python 풀이
```python
from collections import Counter

class Solution:
    def removeDuplicateLetters(self, s: str) -> str:

        stack = []
        counter = Counter(s)
        seen = set()

        for letter in s:
            counter[letter] -= 1

            if letter in seen:
                continue

            while stack and stack[-1] > letter and counter[stack[-1]] > 0:
                seen.remove(stack.pop())

            stack.append(letter)
            seen.add(letter)

        return ''.join(stack)
```
stack만 사용해도 되지만 in으로 빠르게 검색해서 처리하기 위해 set을 하나 추가해서 사용한다.

## Java 풀이
```java
import java.util.HashMap;
import java.util.Map;
import java.util.Stack;

class Solution {
    public String removeDuplicateLetters(String s) {

        // 카운터 초기화
        Map<Character, Integer> counter = new HashMap<>();
        for (char letter : s.toCharArray()) {
            Integer value = counter.getOrDefault(letter, 0);
            counter.put(letter, value + 1);
        }

        Stack<Character> stack = new Stack<>();
        for (char letter : s.toCharArray()) {
            counter.put(letter, counter.get(letter) - 1);
            
            // 중복 문자 무시 
            if (stack.contains(letter))
                continue;

            // 새로운 문자의 경우 스택에서 자신보다 크고, counter에 남아있는 수는 pop
            while (!stack.isEmpty() && stack.peek() > letter && counter.get(stack.peek()) >= 1) {
                stack.pop();
            }
            
            stack.push(letter);
        }

        StringBuilder sb = new StringBuilder();
        while (!stack.isEmpty()) {
            sb.append(stack.pop());
        }
        return sb.reverse().toString();
    }

    public static void main(String[] args) {
        System.out.println(new Solution().removeDuplicateLetters("edebbed"));
    }
}
```
