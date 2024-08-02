[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42748)


## Python 풀이
```python
def solution(array, commands):
    answer = []

    for command in commands:
        partition = array[command[0]-1:command[1]]
        partition.sort()
        answer.append(partition[command[2]-1])
    return answer
```

## Java 풀이
```java
class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        int idx = 0;

        for (int[] command : commands) {
            int start = command[0] - 1;
            int end = command[1];
            int key = command[2] - 1;
            int[] split = Arrays.copyOfRange(array, start, end);

            Arrays.sort(split);
            answer[idx] = split[key];
            idx += 1;
        }
        return answer;
    }

}
```

## Kotlin
```kotlin
class Solution {
    fun solution(array: IntArray, commands: Array<IntArray>): IntArray {
        return commands.map { command ->
            array.slice(IntRange(command[0] - 1, command[1] - 1)).sorted()[command[2] - 1]
        }.toIntArray()
    }
}
```
