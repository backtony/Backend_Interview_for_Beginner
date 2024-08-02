[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42840)


## Python 풀이
```python
def solution(answers):
    answer = []
    length = len(answers)
    students = [[1, 2, 3, 4, 5], [2, 1, 2, 3, 2, 4, 2, 5], [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]]
    correct = [0, 0, 0]
    length1 = len(students[0])
    length2 = len(students[1])
    length3 = len(students[2])
    for idx in range(length):
        if answers[idx] == students[0][idx % length1]:
            correct[0] += 1

        if answers[idx] == students[1][idx % length2]:
            correct[1] += 1

        if answers[idx] == students[2][idx % length3]:
            correct[2] += 1

    top = max(correct)
    for idx in range(3):
        if top == correct[idx]:
            answer.append(idx + 1)

    return answer
```

## Java 풀이
```java
import java.util.ArrayList;
import java.util.Arrays;

class Solution {
    public int[] solution(int[] answers) {
        ArrayList<Integer> answer = new ArrayList<>();

        int length = answers.length;
        int[][] value = {% raw %} {{1, 2, 3, 4, 5}, {2, 1, 2, 3, 2, 4, 2, 5}, {3, 3, 1, 1, 2, 2, 4, 4, 5, 5}} {% endraw %};

        int[] count = new int[3];

        for (int i = 0; i < length; i++) {
            for (int j = 0; j < 3; j++) {
                int idx = i % value[j].length;
                if (answers[i] == value[j][idx]) {
                    count[j] += 1;
                }
            }
        }
        int maxCount = Arrays.stream(count).max().getAsInt();
        for (int i = 0; i < 3; i++) {
            if (count[i] == maxCount)
                answer.add(i + 1);
        }

        return answer.stream().mapToInt(Integer::intValue).toArray();
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(answers: IntArray): IntArray {
        var answer = mutableMapOf<Int, Int>()
        val one = listOf(1, 2, 3, 4, 5)
        val two = listOf(2, 1, 2, 3, 2, 4, 2, 5)
        val three = listOf(3, 3, 1, 1, 2, 2, 4, 4, 5, 5)

        answers.forEachIndexed { index, ans ->

            if (ans == one[index % 5]) {
                answer[1] = answer.getOrDefault(1, 0) + 1
            }

            if (ans == two[index % 8]) {
                answer[2] = answer.getOrDefault(2, 0) + 1
            }

            if (ans == three[index % 10]) {
                answer[3] = answer.getOrDefault(3, 0) + 1
            }

        }

        return answer.entries.filter { it.value == answer.values.maxOrNull() }.map { it.key }.sorted().toIntArray()
    }
}
```
