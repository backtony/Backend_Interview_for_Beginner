[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12916)


## 풀이
```python
from collections import Counter

def solution(s):
    answer = True

    s = s.lower()
    
    cnt = Counter(s)
    if cnt.get("p") != cnt.get("y"):
        answer = False    

    return answer
```