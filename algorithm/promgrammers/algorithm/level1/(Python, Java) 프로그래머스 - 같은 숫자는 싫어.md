[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12906)


## Python 풀이
```python
def solution(arr):
    answer = [arr[0]]

    for num in arr[1:]:
        if num == answer[-1]:
            continue
        else:
            answer.append(num)
    return answer
```

## Java 풀이
```java
import java.util.*;

public class Solution {
    public int[] solution(int[] arr) {
        LinkedList<Integer> answer = new LinkedList<>();
        answer.add(arr[0]);
        for (int i = 1; i < arr.length; i++) {
            if (answer.getLast() != arr[i]) {
                answer.add(arr[i]);
            }
        }

        return answer.stream().mapToInt(Integer::intValue).toArray();
    }
}
```