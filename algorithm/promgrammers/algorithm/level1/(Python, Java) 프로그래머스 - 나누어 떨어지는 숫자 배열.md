[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12910)


## Python 풀이
```python
def solution(arr, divisor):
    arr.sort()
    answer =[x for x in arr if x%divisor==0]
    return answer if answer else [-1]
```

## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public int[] solution(int[] arr, int divisor) {
        int[] answer = Arrays.stream(arr).filter(x -> x % divisor == 0).toArray();
        if (answer.length == 0){
            return new int[]{-1};
        }
        Arrays.sort(answer);
        return answer;
    }
}
```

## Kotlin 풀이
```kotlin
class Solution {
    fun solution(arr: IntArray, divisor: Int): IntArray {
        val result = arr.filter { it % divisor == 0 }.sorted().toIntArray()

        if (result.isEmpty()) {
            return listOf(-1).toIntArray()
        }
        return result
    }
}
```
