[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17682)


## Python 풀이
```python
def solution(dartResult):
    answer = []
    idx = -1
    dartResult = dartResult.replace('10', 't')
    bonus = ["S", "D", "T"]
    games = ["10" if x == 't' else x for x in dartResult]

    for game in games:
        if game in bonus:
            answer[idx] **= bonus.index(game) + 1
        elif game == "*":
            answer[idx] *= 2
            if idx != 0:
                answer[idx - 1] *= 2
        elif game == "#":
            answer[idx] *= -1

        else:
            answer.append(int(game))
            idx += 1

    return sum(answer)
```
주어지는 문자열이 10을 제외하면 모두 1문자로 의미가 정해진다. 따라서 10만 한 문자로 처리한 뒤 split하고 연산을 진행하면 된다.  

## Python 정규식 풀이
```python
import re

def solution(dartResult):    
    # ()를 기준으로 각 자리에 대한 정규식 정의
    # d+ 숫자로 이뤄지고, 숫자 이후에는 SDT 중 하나 그 뒤에는 #,*가 있거나 없거나
    # findall은 정규식에 매칭되는 것들을 substring해서 만들고 리스트로 반환해준다.
    # substring 한다는 의미는 ()괄호마다 매핑되는 것을 자른다는 의미
    results = re.findall('(\d+)([SDT])([*#]?)', dartResult)
    bonus = {"S": 1, "D": 2, "T": 3}
    price = {"": 1, "*": 2, "#": -1}
    answer = []
    for idx, result in enumerate(results):
        score, bonus_num, price_num = result
        current_score = int(score) ** bonus[bonus_num] * price[price_num]
        if price[price_num] == 2 and idx >= 1:
            answer[idx - 1] *= price[price_num]
        answer.append(current_score)
    return sum(answer)    
```
앞선 풀이 방식은 두 자리 문자열이 의미를 가지는 것이 10만 있기 때문에 가능한 풀이다.  
만약 10, 11, 12 까지 처리해야된다면 처리하기 번거로워진다.  
정규식을 이용하면 원하는 대로 split해서 자를 수 있다.

## Python 풀이
```python
def solution(dartResult):
    dart = {'S':1, 'D':2, 'T':3}
    scores = []
    n = 0

    for i, d in enumerate(dartResult):
        if d in dart:
            scores.append(int(dartResult[n:i])**dart[d])
        if d == "*":
            scores[-2:] = [x*2 for x in scores[-2:]]
        if d == "#":
            scores[-1] = (-1)*scores[-1]
        if not (d.isnumeric()):
            n = i+1

    return sum(scores)
```
정규식을 사용하기 싫다면 이렇게 풀어도 될것 같다.  
n에 숫자 시작점을 기억하고 S,D,T가 나오면 거기까지 해서 잘라 숫자를 구하는 방식이다.

## Java 풀이
```java
class Solution {
    public int solution(String dartResult) {
        String results = dartResult.replaceAll("10", "t");
        List<Character> bonus = List.of('S', 'D', 'T');

        List<Integer> scores = new ArrayList<>();
        int idx = -1;

        for (char ch : results.toCharArray()) {
            if (ch == 't' || Character.isDigit(ch)) {
                if (ch == 't') {
                    scores.add(10);
                } else {
                    scores.add(Character.getNumericValue(ch));
                }
                idx += 1;
            } else if (bonus.indexOf(ch) != -1) {
                scores.set(idx, (int) Math.pow(scores.get(idx), bonus.indexOf(ch) + 1));
            } else {
                Integer currentScore = scores.get(idx);
                if (ch == '*') {
                    scores.set(idx, currentScore * 2);
                    if (idx >= 1) {
                        Integer beforeScore = scores.get(idx - 1);
                        scores.set(idx - 1, beforeScore * 2);
                    }
                } else {
                    scores.set(idx, -currentScore);
                }
            }
        }
        return scores.stream().mapToInt(Integer::intValue).sum();
    }
}
```
List 자료구조는 get해서 수정하는게 아니라 set으로 수정한다는 것을 기억하자.