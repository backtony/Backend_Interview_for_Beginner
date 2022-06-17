[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42584)


## Python 풀이
```python
def solution(prices):
    length = len(prices)

    # answer을 max값으로 초기화  
    answer = [i for i in range(length - 1, -1, -1)]

    # 주식 가격이 떨어질 경우 찾기
    stack = [0]
    for i in range(1, length):
        while stack and prices[stack[-1]] > prices[i]:
            j = stack.pop()
            answer[j] = i - j
        stack.append(i)
    return answer
```
문제의 관심사는 떨어지지 않은 기간이다. 기간을 알 수 있는 것은 인덱스 차이로 귀결되므로 스택에 넣어야 하는 것은 인덱스이다.  
스택에 보통 값을 넣기 때문에 인덱스를 넣어서 풀이한다는 것이 생각해내기 어려울 수 있다.  

## Java 풀이
```java
import java.util.Stack;

class Solution {
    public int[] solution(int[] prices) {
        int length = prices.length;

        // 최대 길이로 초기화
        int[] answer = new int[length];
        for (int idx = 0; idx < length; idx++) {
            answer[idx] = length - idx - 1;
        }

        // stack으로 가격이 떨어지는 지점에 대한 수정
        Stack<Integer> stack = new Stack<>();
        for (int idx = 0; idx < length; idx++) {
            while (!stack.isEmpty() && prices[stack.peek()] > prices[idx]) {
                Integer popIdx = stack.pop();
                answer[popIdx] = idx - popIdx;
            }
            stack.add(idx);
        }
        
        return answer;
    }
}
```






