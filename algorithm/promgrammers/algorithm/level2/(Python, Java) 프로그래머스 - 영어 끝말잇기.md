[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12981)


## Python 풀이
```python
import math


def solution(n, words):
    answer = [0, 0]

    words_store = set()

    for idx, word in enumerate(words):
        if idx == 0:
            words_store.add(word)
            prev = word[-1]
            continue

        if word in words_store or prev != word[0]:
            answer[0] = (idx % n) + 1
            answer[1] = math.ceil((idx + 1) / n)
            break

        words_store.add(word)
        prev = word[-1]

    return answer
```

## Java 풀이
```java
import java.util.Arrays;
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int[] solution(int n, String[] words) {
        int[] answer = new int[2];
        Arrays.fill(answer, 0);
        Set<String> usedWords = new HashSet<>();
        char prev = 0;

        for (int idx = 0; idx < words.length; idx++) {
            if (idx == 0) {
                usedWords.add(words[idx]);
                prev = words[idx].charAt(words[idx].length() - 1);
                continue;
            }

            if (usedWords.contains(words[idx]) || prev != words[idx].charAt(0)) {
                answer[0] = (idx % n) + 1;
                answer[1] = (int) Math.ceil((idx + 1) / (double) n);
                break;
            }

            usedWords.add(words[idx]);
            prev = words[idx].charAt(words[idx].length() - 1);
        }

        return answer;
    }
}
```


