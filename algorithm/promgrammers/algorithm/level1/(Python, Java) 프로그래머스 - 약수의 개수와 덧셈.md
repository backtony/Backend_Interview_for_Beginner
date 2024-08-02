[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/77884)


## Python 풀이1
```python
import math


def divisorCount(x):
    count = 0
    end = (int)(math.sqrt(x))
    for i in range(1, end + 1):
        if x % i == 0 and i ** 2 == x:
            count += 1
        elif x % i == 0:
            count += 2
    return count


def solution(left, right):
    answer = 0

    for i in range(left, right + 1):
        if divisorCount(i) % 2 == 0:
            answer += i
        else:
            answer -= i
    return answer
```

## Python 풀이2
```python
import math

def solution(left, right):
    answer = 0
    for i in range(left, right + 1):
        if int(math.sqrt(i)) == math.sqrt(i):
            answer -= i
        else:
            answer += i
    return answer

```

## Java 풀이
```java
class Solution {
    public int solution(int left, int right) {
        int answer = 0;

        for (int target = left; target <= right; target++) {
            // 약수의 개수가 홀수인 경우는 제곱근인 경우 뿐이 없다.
            if (target % Math.sqrt(target) == 0) {
                answer -= target;
            } else {
                answer += target;
            }
        }
        return answer;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.solution(13, 17));
    }

}
```

## kotlin 풀이
```kotlin
import kotlin.math.sqrt

class Solution {
    fun solution(left: Int, right: Int): Int {
        var answer = 0

        for (target in left..right) {
            if (isOdd(target)) {
                answer -= target
            } else {
                answer += target
            }
        }

        return answer
    }

    private fun isOdd(target: Int): Boolean {
        val sqrt = sqrt(target.toDouble())

        return target % sqrt == 0.0
    }
}
```
