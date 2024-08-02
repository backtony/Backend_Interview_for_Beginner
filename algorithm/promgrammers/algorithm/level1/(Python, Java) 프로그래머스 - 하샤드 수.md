[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12947)


## Python 풀이
```python
def solution(x):
    return True if x % sum(map(int, str(x))) == 0 else False
```

## Java 풀이
```java
class Solution {
    public boolean solution(int x) {
        boolean answer = false;
        int sum = 0;
        for (char ch : String.valueOf(x).toCharArray()) {
            sum += Character.getNumericValue(ch);
        }
        if (x % sum == 0)
            answer = true;

        return answer;
    }
}
```


## kotlin 풀이
```kotlin
class Solution {
    fun solution(x: Int): Boolean {

        val sum = x.toString().map {
            it.digitToInt()
        }.sum()

        if (x % sum == 0) {
            return true
        }

        return false
    }
}
```
