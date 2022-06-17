[문제 링크](https://programmers.co.kr/learn/challenges?tab=all_challenges)


## Python 풀이
```python
def solution(A, B):
    answer = 0
    A.sort()
    B.sort()
    length = len(A)

    for idx in range(length):
        answer += A[idx] * B[length - idx - 1]

    return answer
```

## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public int solution(int[] A, int[] B) {
        Arrays.sort(A);
        Arrays.sort(B);

        int total = 0;
        int length = A.length;
        for (int idx = 0; idx < length; idx++) {
            total += A[idx] * B[length - idx - 1];
        }

        return total;
    }
}
```