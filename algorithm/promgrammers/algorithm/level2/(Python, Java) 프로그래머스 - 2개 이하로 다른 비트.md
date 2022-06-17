[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/77885)


## Python 풀이
```python
def solution(numbers):
    answer = []
    for num in numbers:
        # 짝수
        # 짝수는 이진수로 1의 자리수가 항상 0이므로 1을 더해주면 답안 조건에 맞는다.
        if num % 2 == 0:
            answer.append(num + 1)
        # 홀수
        # 오른쪽에서 0을 찾아서 1로 바꿔주고 그 전자리를 0으로 바꿔준다.
        else:
            tmp = "0" + bin(num)[2:]
            idx = tmp.rfind('0')
            tmp = list(tmp)
            tmp[idx] = "1"
            tmp[idx + 1] = "0"
            answer.append(int(''.join(tmp), 2))

    return answer
```
전형적인 수학문제다.  
짝수는 이진수로 변환시 항상 첫자리가 0이기 때문에 그 자리를 1로 채워주면 조건에 맞는 답이 나온다.  
홀수는 오른쪽에서부터 0을 찾아서 1로 바꿔주고 그 전에 자리를 0으로 바꿔주면 조건에 맞는 답이 나온다.  
주의해야할 것이 111이면 0을 못찾으므로 맨앞에 0을 더해줘서 연산을 진행한다.  

## Java 풀이
```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public long[] solution(long[] numbers) {
        List<Long> answer = new ArrayList<>();
        for (long number : numbers) {
            if (number % 2 == 0)
                answer.add(number + 1);
            else {
                String binary = "0" + Long.toBinaryString(number);
                char[] temp = binary.toCharArray();
                int idx = binary.lastIndexOf("0");
                temp[idx] = '1';
                temp[idx + 1] = '0';
                answer.add(Long.parseLong(String.valueOf(temp), 2));
            }
        }

        return answer.parallelStream().mapToLong(Long::longValue).toArray();
    }
}
```
