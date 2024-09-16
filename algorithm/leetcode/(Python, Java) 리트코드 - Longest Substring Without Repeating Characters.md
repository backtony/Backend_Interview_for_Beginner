[문제 링크](https://leetcode.com/problems/longest-substring-without-repeating-characters/)


## Python 풀이
```python
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:

        start = max_length = 0
        idx_store = dict()
        for idx, letter in enumerate(s):
            value = idx_store.get(letter)
            if value is None or value < start:
                max_length = max(max_length, idx - start + 1)
            else:
                start = value + 1

            idx_store[letter] = idx

        return max_length
```

## Java 풀이
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int lengthOfLongestSubstring(String s) {

        Map<Character, Integer> idxMap = new HashMap<>();
        int start = 0;
        int maxLength = 0;
        for (int idx = 0; idx < s.length(); idx++) {
            char key = s.charAt(idx);
            if (idxMap.containsKey(key) && idxMap.get(key) >= start) {
                start = idxMap.get(key) + 1;
            } else {
                maxLength = Math.max(maxLength, idx - start + 1);
            }
            idxMap.put(key, idx);
        }

        return maxLength;
    }
}
```


## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun lengthOfLongestSubstring(s: String): Int {
        var temp = ""
        var answer = 0

        for (letter in s) {

            if (temp.contains(letter)) {
                answer = max(answer, temp.length)
                temp = temp.substring(temp.lastIndexOf(letter) + 1) + letter
            } else {
                temp += letter
            }
        }

        return max(answer, temp.length)
    }
}
```
