[문제 링크](https://leetcode.com/problems/longest-repeating-character-replacement/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun characterReplacement(s: String, k: Int): Int {

        val counter = mutableMapOf<Char, Int>()
        var answer = 0
        var left = 0
        for (letter in s) {
            counter[letter] = counter.getOrDefault(letter, 0) + 1

            val total = counter.values.sum()
            val max = counter.values.max()
        
            // K 임계치 꽉참
            // 현재 문자열을 추가해서 문제가 생겼으므로 앞쪽에 하나를 빼면 문제가 사라진다.
            if (total - max > k) {
                counter[s[left]] = counter.getOrDefault(s[left], 0) - 1
                left++
                
            // 문제 없음
            } else {
                answer = max(answer, total)
            }
        }

        return answer
    }
}
```
