[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/82612)


## Python 풀이
```python
def solution(price, money, count):
    answer = 0

    for i in range(1, count + 1):
        answer += price * i

    return 0 if answer <= money else answer - money
```

## Java 풀이
```java
class Solution {
    public long solution(int price, int money, int count) {
        long answer = 0;
        long tot = 0;
        for (int i = 1; i <= count; i++) {
            tot += price * i;
        }

        if (tot > money) {
            answer = tot - money;
        }

        return answer;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(price: Int, money: Int, count: Int): Long {
        var total = 0L
        for (i in 1..count) {
            total += price * i
        }
        
        return if (total < money) {
            0
        } else {
            total.minus(money)
        }
    }
}
```
