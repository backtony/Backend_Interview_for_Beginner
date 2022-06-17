[문제 링크](https://leetcode.com/problems/different-ways-to-add-parentheses/)


## Python 풀이
```python
from typing import List

class Solution:
    # 이 재귀함수는 주어진 expression의 모든 연산 경우의 수를 반환한다.
    def diffWaysToCompute(self, expression: str) -> List[int]:
        def compute(left, right, value):
            results = []
            for l in left:
                for r in right:
                    results.append(eval(str(l) + value + str(r)))
            return results

        if expression.isdigit():
            return [expression]

        results = []
        for idx, unit in enumerate(expression):
            # 기호 나오면
            if unit in ['-', '*', '+']:
                # 왼쪽 잘라서 모든 경우의수 만들고    
                left = self.diffWaysToCompute(expression[:idx])
                # 오른쪽 잘라서 모든 경우의 수 만든다.
                right = self.diffWaysToCompute(expression[idx + 1:])
                # 나온 경우의 수를 가지고 연산한다.
                results.extend(compute(left, right, unit))

        return results
```
재귀함수의 기준을 잡는게 가장 중요하다.  
재귀함수는 깊게 파고들면 절대 쉽게 풀수 없으니 가정 자체가 제일 중요하다.  
문제에서 주어진 바에 따르면 diffWaysToCompute 함수는 주어진 expression에 대해 모든 경우의 수를 구한 배열을 반환한다.  
그렇다면 연산 기호를 중심으로 왼쪽 expression의 모든 연산 경우의 수와 오른쪽 expression의 모든 연산 경우의 수를 나눠서 구하고 현재 연산 기호를 통해 최종적으로 모든 경우의 수를 구할 수 있다.  
재귀를 사용하므로 탈출하는 if문을 잘 고려해서 작성해야 한다.  

## Java 풀이
```java
import java.util.*;

class Solution {
    public List<Integer> diffWaysToCompute(String expression) {
        Set<Character> units = new HashSet<>(List.of('+', '-', '*'));

        if (isDigit(expression)) {
            return new ArrayList<>(List.of(Integer.valueOf(expression)));
        }

        List<Integer> results = new ArrayList<>();
        for (int idx = 0; idx < expression.length(); idx++) {
            char unit = expression.charAt(idx);
            if (units.contains(unit)) {
                List<Integer> left = diffWaysToCompute(expression.substring(0, idx));
                List<Integer> right = diffWaysToCompute(expression.substring(idx + 1));
                results.addAll(compute(left, right, unit));
            }
        }
        return results;
    }

    private boolean isDigit(String expression) {
        for (char letter : expression.toCharArray()) {
            if (!Character.isDigit(letter))
                return false;
        }
        return true;
    }

    private List<Integer> compute(List<Integer> left, List<Integer> right, char unit) {
        List<Integer> results = new ArrayList<>();

        for (Integer l : left) {
            for (Integer r : right) {
                if (unit == '+')
                    results.add(l + r);
                else if (unit == '-')
                    results.add(l - r);
                else
                    results.add(l * r);
            }
        }
        return results;
    }
}
```
