[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12930)


## Python 풀이
```python
def solution(s):
    answer = []
    words = s.split(' ')
    for word in words:
        tmp = ""
        for idx in range(len(word)):
            if idx % 2 == 0:
                tmp += word[idx].upper()
            else:
                tmp += word[idx].lower()

        answer.append(tmp)
    answer = " ".join(answer)

    return answer
```

## Python 풀이 2
```python
def solution(s):
    return " ".join(map(lambda x : ''.join([word.upper() if idx%2 == 0 else word.lower() for idx, word in enumerate(x)]),s.split(' ')))
```
짧긴하나 그다지 가독성이 좋아보이지는 않는다.
enumerate를 사용하여 for로 받으면 인덱스와 해당 값을 한번에 받을 수 있다 정도로 알아두자.

## Java 풀이
```java
class Solution {
    public String solution(String s) {
        StringBuilder sb = new StringBuilder();
        int idx = 0;
        for (char ch : s.toCharArray()) {
            if (ch == ' ')
                idx = 0;
            else {
                ch = idx % 2 == 0 ?
                        Character.toUpperCase(ch) :
                        Character.toLowerCase(ch);
                idx++;
            }
            sb.append(ch);
        }

        return sb.toString();
    }
}
```