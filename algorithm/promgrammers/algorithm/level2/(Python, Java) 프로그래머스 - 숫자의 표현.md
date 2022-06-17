[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12924)


## Python 풀이
```python
def solution(n):
    answer = 0
    sum = 0
    start = 0
    end = 0
    while end <= n:
        if sum < n:
            end += 1
            sum += end
        else:
            if sum == n:
                answer += 1
            start += 1
            sum -= start

    return answer
```
무난한 투포인터 알고리즘이다.  

## Java 풀이
```java
class Solution {
    public int solution(int n) {
        int cnt = 0;
        int start = 0;
        int end = 0;
        int sum = 0;

        while (end <= n) {
            if (sum < n) {
                end += 1;
                sum += end;
            } else {
                if (sum == n) {
                    cnt += 1;
                }
                start += 1;
                sum -= start;
            }
        }

        return cnt;
    }
}
```