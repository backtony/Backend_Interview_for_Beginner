[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12951)


## Python 풀이
```python
def solution(s):
    unit = s.split(" ")
    for idx in range(len(unit)):
        unit[idx] = unit[idx][:1].upper() + unit[idx][1:].lower()
    return ' '.join(unit)
```


## Java 풀이
```java
class Solution {
    public String solution(String s) {
        s = s.toLowerCase();
        String[] unit = s.split("");
        boolean flag = true;

        StringBuilder sb = new StringBuilder();
        for (String letter : unit) {

            if (letter.equals(" ")) {
                flag = true;

            } else if (flag) {
                letter = letter.toUpperCase();
                flag = false;
            }

            sb.append(letter);
        }

        return sb.toString();
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(s: String): String {
        return s.split(" ").joinToString(" ") {
            if (it.length > 1) {
                it.first().uppercase().plus(it.substring(1).lowercase())
            } else {
                it.uppercase()
            }
        }
    }
}
```
