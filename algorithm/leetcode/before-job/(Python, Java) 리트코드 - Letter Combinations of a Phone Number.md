[문제 링크](https://leetcode.com/problems/letter-combinations-of-a-phone-number/)


## Python 풀이
```python
from typing import List
from itertools import product


class Solution:
    def letterCombinations(self, digits: str) -> List[str]:

        if len(digits) == 0:
            return []

        phone = {"2": ["a", "b", "c"], "3": ["d", "e", "f"], "4": ["g", "h", "i"], "5": ["j", "k", "l"],
                 "6": ["m", "n", "o"], "7": ["p", "q", "r", "s"], "8": ["t", "u", "v"], "9": ["w", "x", "y", "z"]
                 }
        
        ls = []
        for num in digits:
            ls.append(phone.get(num))
        
        answer=[]
        for letters in product(*ls):
            answer.append(''.join(letters))

        return answer
```

## Java 풀이
```java
import java.util.ArrayList;
import java.util.List;
import java.util.Map;

class Solution {

    List<String> answer = new ArrayList<>();
    Map<Character, String> letters = Map.of(
            '2', "abc", '3', "def", '4', "ghi", '5', "jkl",
            '6', "mno", '7', "pqrs", '8', "tuv", '9', "wxyz");

    public List<String> letterCombinations(String digits) {
        if (digits.length() == 0)
            return answer;

        dfs(digits, 0, "");

        return answer;
    }

    private void dfs(String digits, int idx, String result) {
        if (digits.length() == idx) {
            answer.add(result);
            return;
        }

        for (char letter : letters.get(digits.charAt(idx)).toCharArray()) {
            dfs(digits, idx + 1, result + letter);
        }
    }
}
```
파이썬으로는 쉽게 풀었지만 자바로는 항상 순열, 조합 문제는 어려운 것 같다.  


## kotlin
```kotlin
class Solution {
    fun letterCombinations(digits: String): List<String> {
        if (digits.isBlank()) {
            return emptyList()
        }

        val letters = mapOf(
            '2' to "abc".toCharArray(),
            '3' to "def".toCharArray(),
            '4' to "ghi".toCharArray(),
            '5' to "jkl".toCharArray(),
            '6' to "mno".toCharArray(),
            '7' to "pqrs".toCharArray(),
            '8' to "tuv".toCharArray(),
            '9' to "wxyz".toCharArray()
        )

        val arrayList = digits.map { letters[it]!! }

        return combinations(arrayList)
    }

    private fun combinations(arrayList: List<CharArray>): List<String> {
        val answer = mutableListOf<String>()

        fun comb(arrayList: List<CharArray>, current: List<Char>) {
            if (arrayList.isEmpty()) {
                answer.add(current.joinToString(""))
                return
            }

            for (letter in arrayList.first()) {
                comb(arrayList - arrayList.first(), current + letter)
            }
        }

        comb(arrayList, listOf())
        return answer
    }
}
```
