[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12985)


## Python 풀이
```python
def solution(n, a, b):
    answer = 0
    while a != b:
        a = (a + 1) // 2
        b = (b + 1) // 2
        answer += 1

    return answer
```
무난한 규칙 찾는 문제다.  
각 숫자에 1을 더해서 2로 나누면 다음 스테이지에서의 번호가 나온다.  
해당 숫자가 같아질 때까지 진행하면 된다.

## Java 풀이
```java
class Solution {
    public int solution(int n, int a, int b) {
        int answer = 0;

        while (a != b) {
            a = (a + 1) / 2;
            b = (b + 1) / 2;
            answer++;
        }

        return answer;
    }
}
```



