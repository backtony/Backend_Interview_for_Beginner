[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12943)


## Python 풀이
```python
def solution(num):
    cnt = 0
    while cnt != 500 and num != 1:
        if num % 2 == 0:
            num //= 2
        else:
            num = num * 3 + 1
        cnt += 1

    return cnt if cnt != 500 else -1
```

## Java 풀이
```java
class Solution {
    public int solution(int num) {
        int answer = 0;
        long n = (long) num;
        while (n != 1) {
            if (answer >= 500) {
                return -1;
            }
            n = (n % 2 == 0) ? n / 2 : n * 3 + 1;
            answer += 1;
        }
        return answer;
    }
}
```
3배하는 과정에서 int 범위를 초과하는 경우가 있기 때문에 long으로 형변환을 한 뒤에 진행해야 한다.

## Kotlin 풀이
```kotlin
class Solution {
    fun solution(num: Int): Int = collatzAlgorithm(num.toLong(), 0)

    tailrec fun collatzAlgorithm(num: Long, cnt: Int): Int =
        when {
            cnt > 500 -> -1
            num == 1L -> cnt
            else -> collatzAlgorithm(if (num % 2 == 0L) num / 2 else (num * 3) + 1, cnt + 1)
        }
}
```
tailrec은 꼬리재귀 일때 사용한다. 컴파일 시에 while 대신 for 루프로 처리해주기 때문에 재귀함수가 호출되면서 소비되는 스택을 아낄 수 있다.
