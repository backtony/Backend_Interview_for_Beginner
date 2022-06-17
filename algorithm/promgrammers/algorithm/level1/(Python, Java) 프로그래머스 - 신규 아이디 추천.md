
[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/72410)


## 풀이
```python
import re


def solution(new_id):
    answer = new_id.lower()  
    answer = re.sub("[^a-z\d.\-_]", "", answer)
    answer = re.sub("\\.+", ".", answer)
    answer = re.sub("^[.]|[.]$", "", answer)

    if len(answer) == 0:
        answer = "a"

    if len(answer) >= 16:
        answer = answer[:15]

    answer = re.sub("[.]$", "", answer)
    while len(answer) <= 2:
        answer += answer[-1]

    return answer


print(solution("abcdefghijklmn.p"))

```
sub api는 인자로 정규식, 교체값, 대상을 받는다.  
정규식에 매칭되는 문자열을 교체값으로 교체해주고 문자열을 반환한다.  
[] 괄호는 문자 클래스로 안에 있는 것들은 문자로 인식한다.  
문자 클래스 안에서 -는 사이값을 의미하므로 -문자를 포함하고 싶다면 맨 마지막에 넣거나 이스케이프 처리해야한다.  

## Java 풀이
```java
class Solution {
    public String solution(String new_id) {
        String answer = "";
        answer = new_id.toLowerCase();
        answer = answer.replaceAll("[^a-z\\d._-]+", ""); // []안의 문자는 문자로 인식한다. 이스케이프로 시작하는 예약어 아니면 그냥 문자로 인식한다.
        answer = answer.replaceAll("\\.+", "."); // .은 예약어이므로 이스케이프로 문자 .임을 알린다.
        answer = answer.replaceAll("^[.]|[.]$", "");

        if (answer.isBlank()) {
            answer = "a";
        }
        if (answer.length() >= 16) {
            answer = answer.substring(0, 15);
        }
        answer = answer.replaceAll("[.]$", "");

        while (answer.length() <= 2) {
            answer += answer.charAt(answer.length() - 1);
        }
        return answer;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        solution.solution("123_...de...\nf..");
    }
}
```
자바 정규식은 파이썬 정규식과 달리 \\\\ 이스케이프 문자를 2개 사용해야 \로 인식한다.  
[] 괄호는 문자 클래스로 안에 있는 것들은 문자로 인식한다.  
문자 클래스 안에서 -는 사이값을 의미하므로 -문자를 포함하고 싶다면 맨 마지막에 넣거나 이스케이프 처리해야한다.
