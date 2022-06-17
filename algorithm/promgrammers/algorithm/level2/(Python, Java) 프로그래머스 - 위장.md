[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42578)


## 풀이
```python
from collections import defaultdict

def solution(clothes):
    pool = defaultdict(list)

    for cloth in clothes:
        pool[cloth[1]].append(cloth[0])

    answer = 1
    for kind in pool.values():
        answer *= len(kind) + 1

    return answer - 1
```
Combination을 사용하면 1번 테스트케이스에서 시간 초과가 발생한다.  
로직은 분명 깔끔한데 시간초과가 뜨는 것을 보니 Combination 사용으로 인한 문제라고 생각했고, 다른 방식으로 풀어야한다는 것을 확인했다.  
생각해보니 옷을 안입는 수까지 더해서 전부 곱해준 다음 마지막에 전부 안 입는 경우 1번을 빼면 combination 없이 해결할 수 있었다.




## Java 풀이
```java
import java.util.HashMap;

class Solution {
    public int solution(String[][] clothes) {
        HashMap<String, Integer> clothCount = new HashMap<>();

        for (String[] clothe : clothes) {
            Integer cnt = clothCount.getOrDefault(clothe[1], 0);
            clothCount.put(clothe[1], cnt + 1);
        }

        int answer = 1;
        for (Integer cnt : clothCount.values()) {
            answer *= cnt + 1;
        }

        return answer - 1;
    }
}
```
