[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/92335)


## Python 풀이
```python
import math

def solution(n, k):
    answer = 0
    n = convert_to_k(n, k)
    for num in n.split('0'):
        if num and is_prime(int(num)):
            answer += 1
    return answer


def convert_to_k(n, k):
    answer = ""
    while n >= k:
        answer += str(n % k)
        n //= k
    answer += str(n)
    return answer[::-1]


def is_prime(digit):
    if digit == 1:
        return False

    answer = True

    for i in range(2, int(math.sqrt(digit)) + 1):
        if digit % i == 0:
            answer = False
            break

    return answer
```

## Java 풀이
```java
class Solution {
    public int solution(int n, int k) {

        int cnt = 0;
        String convertedN = convertNToK(n, k);

        for (String num : convertedN.split("0")) {
            if (!num.isBlank() && isPrime(Long.parseLong(num))) {
                cnt += 1;
            }
        }
        return cnt;
    }

    private String convertNToK(int n, int k) {
        StringBuilder sb = new StringBuilder();
        while (n >= k) {
            sb.append(n % k);
            n /= k;
        }
        return sb.append(n).reverse().toString();
    }

    private boolean isPrime(long num) {
        if (num == 1)
            return false;

        for (long i = 2; i < (long) (Math.sqrt(num)) + 1; i++) {
            if (num % i == 0)
                return false;
        }
        return true;
    }
}
```
진수 변환 후 값이 int의 범위를 넘어가는 테스트케이스가 있으므로 Long을 사용해야 한다.
