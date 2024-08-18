[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/72412)


## 풀이
```python
from itertools import combinations
from bisect import bisect_left
import copy


def solution(info, query):
    answer = []
    pool = dict()

    for datas in info:
        datas = datas.split()
        score = int(datas[-1])

        for cnt in range(5):
            for comb in combinations(range(4), cnt):
                tmp = copy.deepcopy(datas[:-1])
                for idx in comb:
                    tmp[idx] = '-'

                key = ''.join(tmp)
                if key in pool:
                    pool.get(key).append(score)
                else:
                    pool[key] = [score]

    for key in pool.keys(): # query에서 sort하게 되면 시간 초과
        pool[key].sort()

    for datas in query:
        datas = datas.replace('and', '').split()

        targetScore = int(datas[-1])
        key = ''.join(datas[:-1])

        targetPeople = pool.get(key) # 없는 경우 None이 나옴
        if targetPeople:
            answer.append(len(targetPeople) - bisect_left(targetPeople, targetScore))
        else:
            answer.append(0)

    return answer
```
범위가 크기 때문에 일일이 처리는 못하고 해시값으로 꺼내와서 처리해야한다는 생각이 처음에 들었다.  
사람이 몇명인가 체크해야하기 때문에 분명 정렬하여 해당 점수보다 큰 점수를 갖는 사람들의 수를 구해야할 것이라는 생각도 들었다.  
그렇다면 해당 조건에 맞는 사람들의 점수를 하나의 리스트에 각각 갖고 있어야 한다는 뜻이다.  
결론은 info로 들어오는 정보가 검색에 포함될 수 있는 모든 방향으로 조합해서 key를 만들고 해시값으로 저장해두고 value로 점수를 주는 형식으로 작성했다.  



