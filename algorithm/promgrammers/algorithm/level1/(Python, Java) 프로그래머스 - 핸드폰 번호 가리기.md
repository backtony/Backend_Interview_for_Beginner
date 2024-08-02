[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12948)


## Python 풀이
```python
def solution(phone_number):
    cnt = len(phone_number)
    return "*" * (cnt - 4) + phone_number[cnt - 4:]
```

## Java 풀이
```java
class Solution {
    public String solution(String phone_number) {
        StringBuilder sb = new StringBuilder();
        int length = phone_number.length();
        for (int i = 0; i < length - 4; i++)
            sb.append("*");
        sb.append(phone_number.substring(length - 4));
        return sb.toString();

    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(phone_number: String): String {
        return "*".repeat(phone_number.length-4).plus(phone_number.takeLast(4))
    }
}
```
