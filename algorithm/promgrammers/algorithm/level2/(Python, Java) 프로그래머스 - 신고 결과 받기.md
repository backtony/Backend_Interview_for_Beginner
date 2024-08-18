[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/92334)


## Python 풀이
```python
def solution(id_list, report, k):
    answer = []
    diction = dict()

    # diction 초기화
    for id in id_list:
        # 신고한 사람, 이메일 받을 카운트
        diction[id] = [set(), 0]

    # 신고한 유저 추가
    for rep in report:
        rep = rep.split()
        user = rep[0]
        villain = rep[1]
        diction.get(villain)[0].add(user)

    # k 이상인 경우 이메일 카운트 업데이트
    for data in diction.values():
        if len(data[0]) >= k:
            for name in data[0]:
                diction.get(name)[1] += 1

    # email 카운트 입력
    for id in id_list:
        answer.append(diction.get(id)[1])

    return answer
```



## Java 풀이
```java
import java.util.HashSet;
import java.util.Set;
import java.util.concurrent.ConcurrentHashMap;

class Solution {
    public int[] solution(String[] id_list, String[] report, int k) {
        int answerLength = id_list.length;
        int[] answer = new int[answerLength];
        ConcurrentHashMap<String, User> map = new ConcurrentHashMap<>();
        // 초기화
        for (String id : id_list) {
            map.put(id, new User());
        }

        // 자신을 신고한 사람 추가
        for (String rep : report) {
            String[] tmp = rep.split(" ");
            String user = tmp[0];
            String villain = tmp[1];
            map.get(villain).email.add(user);
        }

        // 이메일 받을 카운트 업데이트
        for (User user : map.values()) {
            if (user.email.size() >= k) {
                for (String id : user.email) {
                    map.get(id).emailCount += 1;
                }
            }
        }

        // emailCount 추출
        for (int idx = 0; idx < answerLength; idx++) {
            answer[idx] = map.get(id_list[idx]).emailCount;
        }

        return answer;
    }

    class User {
        private Set<String> email = new HashSet<>();
        private int emailCount = 0;
    }
}
```

## Java Stream 풀이
```java
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.stream.Collectors;

class Solution {
    public int[] solution(String[] id_list, String[] report, int k) {
        // 중복 제거
        List<String> list = Arrays.stream(report).distinct().collect(Collectors.toList());
        HashMap<String, Integer> count = new HashMap<>();

        // 신고 당한 횟수 업데이트
        for (String s : list) {
            String target = s.split(" ")[1];
            count.put(target, count.getOrDefault(target, 0) + 1);
        }

        return Arrays.stream(id_list).map(_user -> {
            final String user = _user;
            List<String> reportList = list.stream().filter(s -> s.startsWith(user + " ")).collect(Collectors.toList());
            return reportList.stream().filter(s -> count.getOrDefault(s.split(" ")[1], 0) >= k).count(); // long 반환
        }).mapToInt(Long::intValue).toArray(); // Long타입을 int로 변환시키고 배열로 반환
    }
}
```
시간이 좀 오래걸린다.

## kotlin 풀이
```kotlin
class Solution {
    fun solution(id_list: Array<String>, report: Array<String>, k: Int): IntArray {

        val abusers = mutableMapOf<String,MutableSet<String>>()
        report.forEach {
            val (reporter, abuser) = it.split(" ")
            abusers[abuser] = abusers.getOrDefault(abuser, mutableSetOf()).apply { add(reporter) }
        }

        // associate 연산은 linkedHashMap을 리턴
        val idMap = id_list.associateWith { 0 }
            .toMutableMap()

        abusers.filter { it.value.size >= k }
            .forEach { abuser ->
                abuser.value.forEach {
                    idMap[it] = idMap.getValue(it) + 1
                }
            }

        return idMap.values.toIntArray()
    }
}
```
