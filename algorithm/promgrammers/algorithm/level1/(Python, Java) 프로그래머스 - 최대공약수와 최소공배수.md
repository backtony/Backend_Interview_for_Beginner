[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12940)


## Python 풀이
```python
import math

def solution(n, m):
    gcd = math.gcd(n, m)
    answer = [gcd, n * m // gcd]

    return answer
```
전형적인 수학문제로 그다지 영양가가 있는 문제는 아닌 것 같다.  
math 라이브러리에 gcd를 이용하면 최대 공약수를 구할 수 있고 원래 lcm을 이용하면 최소 공배수를 구할 수 있다.  
하지만 lcm 사용을 막아논 것 같다.  
두 수의 곱을 최대 공약수로 나누면 최소 공배수를 얻을 수 있다. 

## Java 룰이
```java
class Solution {
    public int[] solution(int n, int m) {
        int[] answer = new int[2];
        BigInteger gcd = BigInteger.valueOf(n).gcd(BigInteger.valueOf(m));
        answer[0] = gcd.intValue();
        answer[1] = (n * m) / gcd.intValue();
        return answer;
    }
}
```