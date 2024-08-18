[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/60057)


## Python 풀이
```python
def solution(s):
    length = len(s)
    answer = length

    for cut in range(1, length // 2 + 1):
        duplicateCount = 1
        idx = 0
        tmp = ""
        while idx < length:
            if s[idx:idx + cut] == s[idx + cut:idx + cut * 2]:
                duplicateCount += 1
            elif duplicateCount == 1:
                tmp += s[idx:idx + cut]
            else:
                tmp += str(duplicateCount) + s[idx:idx + cut]
                duplicateCount = 1

            idx += cut

        answer = min(answer, len(tmp))

    return answer
```
문자열의 경우 out of index가 적용되지 않기 때문에 넘어가는 인덱스의 경우 무시된다.

## Java 풀이
```java
class Solution {
    public int solution(String s) {
        int length = s.length();
        int answer = length;

        for (int unit = 1; unit <= length / 2; unit++) {
            int tempLength = 0, idx = 0, cnt = 1;
            while (idx + unit * 2 <= length) {
                if (s.substring(idx, idx + unit).equals(s.substring(idx + unit, idx + unit * 2))) {
                    cnt++;
                } else if (cnt == 1) {
                    tempLength += unit;
                } else {
                    tempLength += String.valueOf(cnt).length() + unit;
                    cnt = 1;
                }
                idx += unit;
            }
            if (idx < length) {
                if (cnt >= 2) {
                    tempLength += String.valueOf(cnt).length() + unit;
                    tempLength += length - (idx + unit);
                } else {
                    tempLength += length - idx;
                }
            }
            answer = Math.min(tempLength, answer);
        }
        return answer;
    }
}
```
자바의 경우 substring이 out of index가 발생하면 안되므로 이에 대한 처리가 따로 필요했다.

## kotlin 풀이
```kotlin
class Solution {
    fun solution(s: String): Int {
        var answer = Int.MAX_VALUE
        for (cnt in 1..s.length) {
            var letter = ""
            var idx = 0
            var buffer = ""
            var duplicated = 1
            while (idx < s.length) {
                if (idx + cnt > s.length) {
                    buffer += s.slice(idx..s.lastIndex)
                    break
                }
                val slice = s.slice(idx until idx + cnt)
                if (slice == buffer) {
                    duplicated++
                } else {
                    if (duplicated > 1) {
                        letter += duplicated.toString() + buffer
                    } else {
                        letter += buffer
                    }

                    duplicated = 1
                    buffer = slice
                }
                idx += cnt
            }

            if (duplicated > 1) {
                letter += duplicated.toString() + buffer
            } else {
                letter += buffer
            }

            answer = Math.min(answer, letter.length)
        }

        return answer
    }
}
```
