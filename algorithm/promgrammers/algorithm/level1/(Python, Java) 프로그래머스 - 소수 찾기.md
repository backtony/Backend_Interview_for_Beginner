[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12921)


## Python 풀이
```python
import math


def solution(n):
    numbers = [1] * (n + 1)
    numbers[0] = numbers[1] = 0

    for num in range(2, int(math.sqrt(n)) + 1):
        multi = 2
        while num * multi <= n:
            numbers[num * multi] = 0
            multi += 1

    return sum(numbers)
```
에라토스테네스의 체 알고리즘이다.

## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public int solution(int n) {
        int[] prime = new int[n + 1];
        Arrays.fill(prime, 1);
        prime[0] = prime[1] = 0;

        for (int num = 2; num <= (int) Math.sqrt(n) + 1; num++) {
            int multi = 2;
            while (num * multi <= n) {
                prime[num * multi] = 0;
                multi += 1;
            }
        }
        return Arrays.stream(prime).sum();
    }
}
```