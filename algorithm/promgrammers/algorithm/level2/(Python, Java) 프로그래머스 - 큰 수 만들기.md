[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42883)


## Python 풀이
```python
from collections import deque


def solution(number, k):
    q = deque()
    for num in number:
        while q and q[-1] < num and k > 0:
            q.pop()
            k -= 1
        q.append(num)
    q = list(q)
    return ''.join(q[:len(number) - k])
```
큰 수를 만들려면 맨앞자리 수가 크면 된다.  
하나씩 큐에 넣으면서 더 큰수가 오면 큐에서 빼는 형식으로 진행한다.  
1000,1 를 테스트 케이스로 해보면 0이 같은 수라 큐에 계속 쌓인다.  
이렇게 되면 k만큼의 수를 제거하지 못하게 되는데 이는 join할 때 인덱싱으로 자르면 된다.


## Java 풀이
```java
import java.util.Stack;

class Solution {
    public String solution(String number, int k) {
        Stack<Character> stack = new Stack<>();

        for (char letter : number.toCharArray()) {
            while (k != 0 && !stack.isEmpty() && stack.peek() < letter) {
                stack.pop();
                k -= 1;
            }
            stack.add(letter);
        }

        StringBuilder sb = new StringBuilder();
        for (Character letter : stack) {
            sb.append(letter);
        }
        String temp = sb.toString();

        return temp.substring(0, temp.length() - k);
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        solution.solution("1924", 2);
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(number: String, k: Int): String {
        val answer = mutableListOf<Int>()
        var cnt = k
        for (numChar in number) {
            val num = numChar.digitToInt()
            while (cnt > 0 && answer.isNotEmpty() && answer.last() < num) {
                answer.removeLast()
                cnt--
            }
            answer.add(num)
        }

        val tempAnswer = answer.joinToString("")
        return tempAnswer.substring(0, tempAnswer.length - cnt)
    }
}
```

