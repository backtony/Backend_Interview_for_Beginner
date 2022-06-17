[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/92342)


## 풀이
```python
from itertools import combinations_with_replacement


def solution(n, info):
    answer = []
    score = [x for x in range(11)]
    max_value = 0

    for units in combinations_with_replacement(score, n):
        lion_ls = [0] * 11
        for unit in units:
            lion_ls[unit] += 1
        peach = 0
        lion = 0
        for idx in range(11):
            lion_cnt = lion_ls[idx]
            peach_cnt = info[idx]
            if lion_cnt != 0 or peach_cnt != 0:
                if lion_cnt <= peach_cnt:
                    peach += 10 - idx
                else:
                    lion += 10 - idx

        distance = lion - peach
        if lion > peach:
            if distance > max_value:
                max_value = distance
                answer.clear()
                answer.append(lion_ls[::-1])
            elif distance == max_value:
                answer.append(lion_ls[::-1])
                answer.sort(reverse=True)
                answer.pop()

    if answer:
        answer = answer[0][::-1]
    else:
        answer = [-1]

    return answer
```
