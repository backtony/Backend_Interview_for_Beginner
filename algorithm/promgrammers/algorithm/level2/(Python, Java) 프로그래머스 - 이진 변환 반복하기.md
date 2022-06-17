[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/70129)


## Python 풀이
```python
from collections import Counter


def solution(s):
    loop = 0
    cnt = 0
    while len(s) != 1:
        loop += 1
        counter = Counter(s)
        cnt += counter["0"]
        s = bin(counter["1"])[2:]

    return [loop, cnt]
```



## Java 풀이
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int[] solution(String s) {
        int loop = 0;
        int cnt = 0;
        while (!s.equals("1")) {
            Map<Character, Integer> counter = new HashMap<>();
            for (char letter : s.toCharArray()) {
                Integer value = counter.getOrDefault(letter, 0);
                counter.put(letter, value + 1);
            }
            s = Integer.toBinaryString(counter.getOrDefault('1', 0));
            cnt += counter.getOrDefault('0', 0);
            loop++;
        }

        int[] answer = {loop, cnt};
        return answer;
    }
}
```