[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/68644)


## Python 풀이
```python
from itertools import combinations


def solution(numbers):
    answer = []

    for comb in combinations(numbers, 2):
        answer.append(comb[0] + comb[1])

    answer = list(set(answer))
    answer.sort()
    return answer
```

## Java 풀이
```java
class Solution {
    public int[] solution(int[] numbers) {
        Set<Integer> set = new TreeSet<>();
        int length = numbers.length;
        for (int i = 0; i < length - 1; i++) {
            for (int j = i + 1; j < length; j++) {
                set.add(numbers[i] + numbers[j]);
            }
        }
        return set.stream().mapToInt(Integer::intValue).toArray();
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(numbers: IntArray): IntArray {
        var answer = mutableSetOf<Int>()

        val numberCntMap = numbers.groupBy { it }.map { it.key to it.value.size }.toMap()
        val numberSet = numbers.toMutableSet()

        for (i in numberSet) {
            for (j in numberSet) {
                if (i == j && numberCntMap[j] == 1) {
                    break
                }
                answer.add(i + j)
            }
        }
        return answer.sorted().toIntArray()
    }
}
```
