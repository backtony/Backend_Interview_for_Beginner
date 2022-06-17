[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17683)


## 풀이
```python
import heapq

def solution(m, musicinfos):
    q = []
    m = m.replace("A#", "a").replace("C#", "c").replace("D#", 'd').replace("F#", 'f').replace("G#", 'g')
    idx = 0
    for musicinfo in musicinfos:
        start, end, title, melody = musicinfo.split(",")
        time = calculate_time(start, end)
        melody = melody.replace("A#", "a").replace("C#", "c").replace("D#", 'd').replace("F#", 'f').replace("G#", 'g')
        melody_length = len(melody)
        repeat_melody = (time // melody_length) * melody + melody[:time % melody_length]
        if repeat_melody.find(m) >= 0:
            heapq.heappush(q, (-time, idx, title))
            idx += 1

    if len(q) == 0:
        answer = "(None)"
    else:
        answer = heapq.heappop(q)[2]

    return answer


def calculate_time(start, end):
    start_hour, start_min = map(int, start.split(":"))
    end_hour, end_min = map(int, end.split(":"))
    end_time = end_hour * 60 + end_min
    start_time = start_hour * 60 + start_min
    return end_time - start_time
```
split하면 #이 분리되기 때문에 이를 어떻게 알파벳과 묶어서 처리하느냐가 핵심이다.  
간단하게 생각해보면 #이 붙는 경우가 몇가지 없으므로 임의로 특정한 문자로 변환시켜주고 처리하면 된다.  
반환하는 정렬 조건이 2가지인데 우선순위 큐로 처리했다.