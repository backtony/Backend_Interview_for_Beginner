[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17684)


## Python 풀이
```python
def solution(msg):
    answer = []

    # 사전 초기화
    diction = {chr(e + 64): e for e in range(1, 27)}
    index = 27

    while msg:
        next = 1
        length = len(msg)
        while next <= length and msg[:next] in diction:
            output = diction.get(msg[:next])
            next += 1

        answer.append(output)
        diction[msg[:next]] = index
        index += 1
        msg = msg[next - 1:]

    return answer
```

## Java 풀이
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

class Solution {
    public int[] solution(String msg) {

        Map<String, Integer> indexMap = new HashMap<>();
        for (int idx = 0; idx < 26; idx++) {
            indexMap.put(String.valueOf((char) ('A' + idx)), idx + 1);
        }

        int idx = 27;
        List<Integer> answer = new ArrayList<>();

        while (msg.length() != 0) {
            int end = 1;
            int length = msg.length();
            while (end <= length && indexMap.containsKey(msg.substring(0, end))) {
                end++;
            }
            answer.add(indexMap.get(msg.substring(0, end - 1)));

            if (end < length) {
                indexMap.put(msg.substring(0, end), idx);
                idx++;
            }
            msg = msg.substring(end - 1);
        }

        return answer.parallelStream().mapToInt(Integer::intValue).toArray();
    }
}
```