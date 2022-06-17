[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42888)


## Python 풀이
```python
def solution(record):
    answer = []
    nickname = dict()
    for datas in record:
        data = datas.split()
        if data[0] != "Leave":
            nickname[data[1]] = data[2]

    for datas in record:
        data = datas.split()
        if data[0] == "Enter":
            answer.append(nickname.get(data[1]) + "님이 들어왔습니다.")
        elif data[0] == "Leave":
            answer.append(nickname.get(data[1]) + "님이 나갔습니다.")

    return answer
```
딕셔너리 사용법만 알고 있다면 쉽게 풀 수 있다.  

## Java 풀이
```java
class Solution {
    public String[] solution(String[] record) {

        HashMap<String, String> map = new HashMap<>();
        final String IN = "님이 들어왔습니다.";
        final String OUT = "님이 나갔습니다.";

        for (String logs : record) {
            String[] log = logs.split(" ");
            String move = log[0];
            String id = log[1];

            if (!move.equals("Leave")) {
                String nickname = log[2];
                map.put(id, nickname);
            }
        }

        List<String> answer = new ArrayList<>();
        for (String logs : record) {
            String[] log = logs.split(" ");
            String move = log[0];
            String id = log[1];

            if (move.equals("Enter")) {
                answer.add(map.get(id) + IN);
            } else if (move.equals("Leave")) {
                answer.add(map.get(id) + OUT);
            }
        }

        return answer.stream().toArray(String[]::new);
    }
}
```