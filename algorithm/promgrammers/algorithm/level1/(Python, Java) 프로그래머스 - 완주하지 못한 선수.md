[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42576)


## Python 풀이 1
```python
def solution(participant, completion):
    dic = {}
    idx = 0

    for name in participant:
        dic[hash(name)] = name
        idx += hash(name)

    for name in completion:
        idx -= hash(name)

    return dic[idx]
```
선수가 최대 10만명이기 때문에 복잡도를 생각해야 한다.  
completion에 partition 선수가 있는지 없는지 확인해야하고 동명이인이면 인원 수만큼 completion에 있는지 확인해야 한다.  
전형적인 count문제 이므로 탐색속도가 빠른 set과 dic중에 하나를 선택해야 한다.  
하지만 set과 dic만으로는 중복 자체를 제거해버리니 때문에 추가적인 방안을 생각해야 한다.  
각각의 모든 hash값은 완전히 일치하지 않으면 다르다.  
hash값을 key로 하여 이름을 저장하고 해당 key값을 다 더한 뒤 completion에서 각 해쉬값을 빼버리면 최종적으로 완주하지 못한 사람의 해쉬값만 남는다.


## Python 풀이 2
Counter을 이용하면 더욱 간단하게 해결할 수 있다. 
```python
from collections import Counter

def solution(participant, completion):
    answer = Counter(participant) - Counter(completion)

    return list(answer)[0]
```

collections.Counter() 메소드는 iterable 객체 즉, list, dict, set, str, bytes, tuple, range와 같은 반복 가능한 객체의 요소를 카운트하여 각각의 빈도 값을 {요소:빈도} 형태인 __해쉬 테이블형태(카운터 객체)__ 로 반환한다.  
여기서 핵심은 Counter 객체는 연산을 제공한다.  
```python
a = collections.Counter("abc")
print(a) # Counter({'a': 1, 'b': 1, 'c': 1}) 
b = collections.Counter("bcd") 
print(b) # Counter({'b': 1, 'c': 1, 'd': 1})
c = a-b
print(c) # Counter({'a': 1})
d = list(c)
print(d) # ['a']
```
__Counter 객체를 리스트로 형변환 시 count 개수는 제거되고 key값만 나오게 된다.__  
<Br>

이외의 제공 메서드
```python
d = collections.Counter(["hello","hi"])
print(d) # Counter({'hello': 1, 'hi': 1})
print(d.get("hello")) # hello 카운트 값 반환 - > 1

d = collections.Counter("aaabbbcccdde")
print(d) # Counter({'a': 3, 'b': 3, 'c': 3, 'd': 2, 'e': 1})
d = collections.Counter("aaabbbcccdde")
e = d.most_common(3) # 카운트 상위 3개 [(키,카운트),(키,카운트)] 리스트 튜플 원소 형태로 반환
print(e) # [('a', 3), ('b', 3), ('c', 3)]

d = collections.Counter(a=4,b=2,c=-2)
print(d) # Counter({'a': 4, 'b': 2, 'c': -2})
e = list(d.elements()) # elements는 카운트 개수가 양수인 key를 개수만큼 이터레이터로 반환 -> 리스트 형번환 필요
print(e) ['a', 'a', 'a', 'a', 'b', 'b']
```
<br>

## Java 풀이
```java
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Map;

class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        Map<String, Integer> map = new HashMap<>();
        for (String part : participant) {
            map.put(part, map.getOrDefault(part, 0) + 1);
        }
        for (String comp : completion) {
            map.put(comp, map.get(comp) - 1);
        }

        for (String key : map.keySet()) {
            if (map.get(key) == 1) {
                answer = key;
                break;
            }
        }
        return answer;
    }
}
```