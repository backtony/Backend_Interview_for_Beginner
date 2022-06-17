[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/64065)


## Python 풀이
```python
def solution(s):
    answer = []
    duple = set() # 빠른 속도를 위해
    s = s.lstrip('{').rstrip('}').split('},{')
    s.sort(key=len)
    for tokens in s:
        for token in tokens.split(','):
            token = int(token)
            if token not in duple:
                answer.append(token)
                duple.add(token)

    return answer
```
lstrip과 rstrip은 인수로 주어진 문자가 아닌 다른 문자가 나올때까지 왼쪽에서, 오른쪽에서 자릅니다.  

<br>

## Python 풀이 2
```python
import re
from collections import Counter

def solution(s):
    counter = Counter(re.findall('\d+',s))
    answer = [int(num) for num,cnt in sorted(counter.items(),key=lambda x:x[1],reverse=True)]
    return answer
```


## Java 풀이
```java
class Solution {
    public int[] solution(String s) {
        HashMap<Integer, Integer> map = new HashMap<>();
        // 쪼개서 숫자만 남기기
        int[] keys = Arrays.stream(s.substring(2, s.length() - 2).split("\\},\\{|,")).mapToInt(Integer::valueOf)
                .toArray();

        // map에 저장
        for (int key : keys) {
            map.put(key,map.getOrDefault(key,0)+1);
        }

        // value를 기준으로 내림차순으로 key를 뽑아내기
        return map.entrySet().stream().sorted(Comparator.comparingInt((Map.Entry<Integer, Integer> entry) -> entry.getValue()).reversed())
                .map(Map.Entry::getKey)
                .mapToInt(Integer::intValue).toArray();
    }

}
```