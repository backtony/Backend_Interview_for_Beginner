[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12953?language=python3)


## Python 풀이
```python
import math

def solution(arr):
    answer = arr[0]
    for unit in arr[1:]:
        gcd = math.gcd(answer, unit)
        answer = answer * unit // gcd 
    return answer
```
프로그래머스에서 lcm을 지원하지 않는다. 따라서 gcd를 사용해서 구해야 한다.  
최소 공배수는 두 수의 곱에다가 최대공약수를 나눈 수이다.

## Java
```java
import java.math.BigInteger;

class Solution {
    public int solution(int[] arr) {
        int answer = arr[0];
        for (int idx = 1; idx < arr.length; idx++) {

            BigInteger gcd = BigInteger.valueOf(answer).gcd(BigInteger.valueOf(arr[idx]));
            answer = (arr[idx] * answer) / gcd.intValue();
        }
        return answer;
    }
}
```