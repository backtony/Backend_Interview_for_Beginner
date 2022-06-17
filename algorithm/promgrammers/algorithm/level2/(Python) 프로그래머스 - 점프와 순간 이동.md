[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12980)


## 풀이
```python
def solution(n):
    ans = 0

    while n != 1:
        ans += n % 2
        n //= 2

    return ans + 1
```




