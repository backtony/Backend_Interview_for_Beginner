[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/76502)


## 풀이
```python
def solution(s):
    answer = 0
    left = ["{", "[", "("]
    right = ["}", "]", ")"]
    for _ in range(len(s)):
        stack = []
        check = 1
        for unit in s:
            if len(stack) == 0 and unit in right:
                check = 0
                break

            if unit in left:
                stack.append(unit)
            else:
                if right.index(unit) != left.index(stack.pop()):
                    check = 0
                    break

        if check and len(stack) == 0:
            answer += 1
        s = s[1:] + s[0]

    return answer
```






