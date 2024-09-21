[문제 링크](https://leetcode.com/problems/reorder-data-in-log-files/)


## Python 풀이
```python
from typing import List

class Solution:
    def reorderLogFiles(self, logs: List[str]) -> List[str]:
        letter = []
        digit = []
        for log in logs:
            if log.split()[1].isdigit():
                digit.append(log)
            else:
                letter.append(log)
        letter.sort(key=lambda x: (x.split()[1:], x.split()[0]))
        return letter + digit


if __name__ == '__main__':
    print(Solution().reorderLogFiles(["dig1 8 1 5 1", "let1 art can", "dig2 3 6", "let2 own kit dig", "let3 art zero"]))
```
sort하는 부분을 저렇게 해도 된다는 것을 기억하자.  

## Java 풀이
```java
import java.util.Arrays;
import java.util.Comparator;

class Solution {
    public String[] reorderLogFiles(String[] logs) {
        Arrays.sort(logs, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                String[] s1 = o1.split(" ", 2);
                String[] s2 = o2.split(" ", 2);

                boolean s1IsDigit = Character.isDigit(s1[1].charAt(0));
                boolean s2IsDigit = Character.isDigit(s2[1].charAt(0));

                if (!s1IsDigit && !s2IsDigit) {
                    int compare = s1[1].compareTo(s2[1]);
                    if (compare == 0)
                        return s1[0].compareTo(s2[0]);
                    return compare;
                } else if (!s1IsDigit) { // o1이 더 앞에 오고자 한다면 -1
                    return -1;
                } else if (!s2IsDigit) {
                    return 1;
                }
                return 0;
            }
        });
        return logs;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun reorderLogFiles(logs: Array<String>): Array<String> {

        val digitLog = mutableListOf<Log>()
        val charLog = mutableListOf<Log>()

        for (log in logs) {
            val (key, body) = log.split(" ", limit = 2)
            if (body[0].isDigit()) {
                digitLog.add(Log(key, body))
                continue
            }

            charLog.add(Log(key, body))
        }

        charLog.sortWith(
            compareBy<Log> { it.log }.thenBy { it.id }
        )

        return (charLog.map { it.fullLog() } + digitLog.map { it.fullLog() }).toTypedArray()
    }

    data class Log(
        val id: String,
        val log: String,
    ) {
        fun fullLog(): String {
            return "$id $log"
        }
    }
}
```
