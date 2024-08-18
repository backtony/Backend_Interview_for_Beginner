[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42890)


## Python 풀이 1
```python
from itertools import combinations


def solution(relation):
    column = len(relation[0])
    row = len(relation)

    # 모든 조합 키
    combination = []
    for cnt in range(column):
        combination.extend(combinations(range(column), cnt + 1))

    # 유일성
    uniq = []
    for keys in combination:
        rowData = [tuple([data[key] for key in keys]) for data in relation]
        if len(set(rowData)) == row:
            uniq.append(keys)

    # 최소성
    length = len(uniq)
    answer = set(uniq)
    for i in range(length):
        for j in range(i + 1, length):
            intersection = set(uniq[i]) & set(uniq[j])
            if len(intersection) == len(uniq[i]):
                answer.discard(uniq[j])

    return len(answer)
```
범위가 매우 작으므로 복잡도는 고려대상에서 제외해도 된다.  
이렇게 문제가 긴 경우 문제를 제대로 읽어야하고 대부분 문제의 __순서대로__ 로직을 짜면 된다.  
즉, 문제를 위에서부터 하나씩 조건으로 걸어서 짜면 된다는 것이다.  
오히려 복합적으로 생각하면 더욱 어려워 진다.  
문제에서 유일성과 최소성을 만족하는 키의 개수를 구하라고 했다.  
따라서 유일성을 만족하는 키 집합을 찾고 그 안에서 최소성을 만족하는 키 집합을 찾으면 된다.  
<br>

일반적으로 set은 단순 리스트의 경우 인수로 넣을 수 있지만 리스트 안의 요소가 리스트인 경우 set의 인수로 전달할 수 없다.  
따라서 요소가 리스트인 경우 tuple 내장함수를 사용해서 튜플로 바꿔준다.  
집합의 요소 제거 함수에는 remove와 discard가 있는데 remove는 없다면 예외를 뱉어내고 discard는 없어도 예외를 뱉지 않고 넘어간다.  
Combination의 경우 리스트의 extend로 붙이게 되면 튜플 형식으로 들어간다.

## Python 풀이 2
```python
from itertools import combinations


def solution(relation):
    idx_store = []
    answer = 0
    column_len = len(relation[0])
    for cnt in range(1, column_len + 1):
        for comb in combinations(range(0, column_len), cnt):

            if not is_minimum(comb, idx_store):
                continue

            if is_candidate(comb, relation):
                answer += 1
                idx_store.append(comb)

    return answer


def is_minimum(comb, idx_store):
    for idx in idx_store:
        cnt = 0
        for i in idx:
            if i in comb:
                cnt += 1
        if cnt == len(idx):
            return False
    return True


def is_candidate(comb, relation):
    key_store = set()
    for data in relation:
        key = ""
        for idx in comb:
            key += data[idx]

        if key in key_store:
            return False
        key_store.add(key)
    return True
```


## Java 풀이
```java
import java.util.ArrayList;
import java.util.HashSet;
import java.util.LinkedList;
import java.util.List;

class Solution {

    List<List<Integer>> uniqKeyList = new ArrayList<>();
    LinkedList<Integer> uniqKey = new LinkedList<>();

    public int solution(String[][] relation) {

        int column = relation[0].length;

        // 인덱스 번호 초기화
        int[] idx = new int[column];
        for (int i = 0; i < column; i++) {
            idx[i] = i;
        }

        // 유일성 키 찾기
        for (int cnt = 1; cnt <= column; cnt++) {
            uniqKey.clear();
            combination(relation, column, cnt, 0);
        }

        // 최소성 찾기
        List<List<Integer>> answer = new ArrayList<>(uniqKeyList);
        for (int i = 0; i < uniqKeyList.size() - 1; i++) {
            for (int j = i + 1; j < uniqKeyList.size(); j++) {
                
                // 전부 포함해서 가지고 있는지 확인
                int cnt = 0;
                for (Integer k : uniqKeyList.get(i)) {
                    if (uniqKeyList.get(j).contains(k)) {
                        cnt += 1;
                    }
                }
                
                // 전부 포함해서 가지고 있다면 삭제 -> 최소성 위반
                if (cnt == uniqKeyList.get(i).size()) {
                    answer.remove(uniqKeyList.get(j));
                }
            }
        }

        return answer.size();
    }

    private void combination(String[][] relation, int n, int r, int now) {
        if (r == 0) {
            // 유니크한지 검사
            HashSet<String> keySet = new HashSet<>();

            for (String[] data : relation) {
                StringBuilder sb = new StringBuilder();
                for (Integer idx : uniqKey) {
                    sb.append(data[idx]);
                }
                String key = sb.toString();
                if (keySet.contains(key)) {
                    return;
                }
                keySet.add(key);
            }
            uniqKeyList.add(List.copyOf(uniqKey));
            return;
        }

        if (now >= n) {
            return;
        }

        uniqKey.add(now);
        combination(relation, n, r - 1, now + 1);

        uniqKey.pollLast();
        combination(relation, n, r, now + 1);
    }

}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(relation: Array<Array<String>>): Int {
        val answer = mutableSetOf<Set<Int>>()
        val columnCnt = relation.first().size
        val columnNumbers = List(columnCnt) { it }

        for (cnt in 1..columnCnt) {
            // 열 조합
            val combination = combination(columnNumbers, cnt)

            combination.forEach combine@{ columnNums ->
                // 이미 최소키가 있다면
                if (answer.any { columnNums.containsAll(it) }) {
                    return@combine
                }
                val keyCandidates = mutableSetOf<String>()

                relation.forEach { row ->
                    var key = ""
                    columnNums.forEach { num ->
                        key += row[num]
                    }

                    if (key in keyCandidates) {
                        return@combine
                    } else {
                        keyCandidates.add(key)
                    }
                }
                
                // 유일키 등록
                answer.add(columnNums.toSet())
            }
        }

        return answer.size
    }

    fun <T> combination(arr: List<T>, r: Int): List<List<T>> {
        if (arr.size < r) {
            return emptyList()
        }
        val result = mutableListOf<List<T>>()

        fun combine(start: Int, current: List<T>) {
            if (current.size == r) {
                result.add(current)
                return
            }

            for (i in start..arr.lastIndex) {
                combine(i + 1, current + arr[i])
            }
        }
        combine(0, listOf())
        return result
    }
}
```


