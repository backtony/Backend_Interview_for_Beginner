[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/43165)


## 풀이
```python
from itertools import product


def solution(numbers, target):
    units = [(-x, x) for x in numbers]
    answer = list(map(sum, product(*units)))
    return answer.count(target)
```

## Java 풀이
```java
class Solution {
    int n;
    int[] result;
    int answer;

    public int solution(int[] numbers, int target) {
        answer = 0;
        n = numbers.length;
        result = new int[n];
        dfs(0, numbers, target);

        return answer;
    }

    private void dfs(int depth, int[] numbers, int target) {
        if (n == depth) {
            if (Arrays.stream(result).sum() == target)
                answer++;
            return;
        }

        result[depth] = numbers[depth];
        dfs(depth + 1, numbers, target);

        result[depth] = -numbers[depth];
        dfs(depth + 1, numbers, target);
    }
}
```

## kotlin
```kotlin
class Solution {
    fun solution(numbers: IntArray, target: Int): Int {
        var answer = 0
        // 중복 순열을 만들고 계산
        permutationWithDuplicated(listOf("+", "-"), numbers.size).forEach { permutaion ->
            val sum = numbers.zip(permutaion) { number, modifier -> "$modifier$number".toInt() }
                .sum()

            if (sum == target) {
                answer++
            }
        }
        return answer
    }

    fun<T> permutationWithDuplicated(arr:List<T>, r: Int ): List<List<T>> {
        val result = mutableListOf<List<T>>()

        fun permute(current: List<T>){
            if (current.size == r) {
                result.add(current)
                return
            }

            for (element in arr) {
                permute(current + element)
            }
        }

        permute(listOf())
        return result
    }
}
```
