[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/49994)


## 풀이
```python
def solution(dirs):
    answer = 0
    direction = {"U": (-1, 0), "R": (0, 1), "D": (1, 0), "L": (0, -1)}

    visit = set()
    x = y = 0
    for d in dirs:
        dx, dy = direction.get(d)
        px = x + dx
        py = y + dy
        if -5 <= px and px <= 5 and -5 <= py and py <= 5:
            if (x, y, px, py) not in visit:
                answer += 1
                visit.add((x, y, px, py))
                visit.add((px, py, x, y))
            x = px
            y = py

    return answer
```
이동하는 좌표를 집합에서 관리하다 보면 두 쌍의 좌표를 반대로 입력하는 경우가 생긴다.  
이런 경우를 방지하기 위해 두 쌍의 순서를 바꿔서 저장해 처리하도록 한다.