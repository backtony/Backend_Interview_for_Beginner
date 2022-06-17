[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12982)


## Python 풀이
```python
def solution(d, budget):
    answer = 0
    total = 0
    d.sort()
    for value in d:
        total += value
        if budget < total:
            break
        elif budget == total:
            answer += 1
            break
        answer += 1
    return answer
```

## Java 풀이

```java
class Solution {
    public int solution(int[] d, int budget) {
        int answer = 0;
        int total = 0;

        Arrays.sort(d);

        for (int i = 0; i < d.length; i++) {
            if (total + d[i] <= budget) {
                total += d[i];
                answer++;
            } else {
                break;
            }
        }
        return answer;
    }
}
```