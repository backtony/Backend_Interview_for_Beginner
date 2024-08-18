[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/72411)


## Python 풀이
```python
from itertools import combinations
from collections import Counter


def solution(orders, course):
    answer = []
    for cnt in course:
        menu = []
        for order in orders:
            menu += list(combinations(sorted(order), cnt))

        menuCounter = Counter(menu)

        if len(menuCounter) != 0:
            maxCount = menuCounter.most_common(1)[0][1]
            if maxCount != 1:
                answer += [''.join(x) for x in menuCounter if menuCounter[x] == maxCount]

    answer.sort()
    return answer
```
처음에 도대체 왜 예시와 같은 결과가 나오는지 좀 오래 걸렸다.  
문제를 잘 읽어보니 __가장 많이 함께 주문된__ 에서 이해가 안되고 있었던 것이다.  
2개 코스라고 가정했을 때 2개로 만든 세트중에 가장 많이 팔린걸 의미한 말이었다.  
문제를 이해하고 나서는 풀이는 금방 해결했다.  
코딩테스트를 연습하다보면 Counter가 정말 많이 사용되므로 Counter 기능을 잘 익혀두는 것이 중요하다는 것을 느끼는 문제다.  



## Java 풀이
```java
class Solution {

    boolean[] visited;
    Map<String, Integer> courseMap = new HashMap<>();

    public String[] solution(String[] orders, int[] course) {
        List<String> answer = new ArrayList<>();

        // 정렬
        for (int i = 0; i < orders.length; i++) {
            char[] arr = orders[i].toCharArray();
            Arrays.sort(arr);
            orders[i] = String.valueOf(arr);
        }

        // 조합 만들기
        for (int i = 0; i < course.length; i++) {
            for (int j = 0; j < orders.length; j++) {
                int length = orders[j].length();
                if (course[i] <= length) {
                    visited = new boolean[length];
                    combination(orders[j].toCharArray(), 0, course[i]);
                }
            }

            // course 개수의 조합에 따른 최대 개수 조합 추출하기
            if (!courseMap.isEmpty()) {
                Integer max = Collections.max(courseMap.values());
                if (max >= 2) {
                    for (String key : courseMap.keySet()) {
                        if (courseMap.get(key) == max) {
                            answer.add(key);
                        }
                    }
                }
                courseMap.clear();
            }
        }

        Collections.sort(answer);

        return answer.toArray(new String[0]);
    }

    private void combination(char[] order, int start, int r) {
        if (r == 0) {
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < order.length; i++) {
                if (visited[i]) {
                    sb.append(order[i]);
                }
            }
            String course = sb.toString();
            courseMap.put(course, courseMap.getOrDefault(course, 0) + 1);
            return;
        }

        for (int i = start; i < order.length; i++) {
            visited[i] = true;
            combination(order, i + 1, r - 1);            
            visited[i] = false;
        }
    }
}
```

## kotlin 풀이
```kotlin
class Solution {

    fun solution(orders: Array<String>, course: IntArray): Array<String> {

        val answer = mutableListOf<String>()
        course.forEach { cnt ->
            val candidates = mutableMapOf<String, Int>()

            orders.forEach { order ->
                val arr = order.toList().sorted()
                val menues = combination(arr, cnt)

                menues.forEach { menu ->
                    val key = menu.joinToString("")
                    candidates[key] = candidates.getOrDefault(key,0) + 1
                }
            }

            val max = candidates.values.maxOrNull()
            answer.addAll(
                candidates.filter { it.value >= 2 }
                    .filter { it.value == max }
                    .map { it.key }
            )
        }

        return answer.sorted().toTypedArray()
    }

    fun <T> combination(arr: List<T>, r: Int): List<List<T>> {
        if (arr.size < r) {
            return emptyList()
        }

        val result = mutableListOf<List<T>>()
        fun combine(start: Int, currentCombine: List<T>) {
            if (currentCombine.size == r) {
                result.add(currentCombine)
                return
            }

            for (i in start..arr.lastIndex) {
                combine(i+1, currentCombine + arr[i])
            }
        }
        combine(0, listOf())
        return result
    }
}
```

