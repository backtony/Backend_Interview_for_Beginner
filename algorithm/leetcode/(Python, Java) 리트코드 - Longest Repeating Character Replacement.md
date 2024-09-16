---
layout: post
title:  (Python, Java) 리트코드 - Longest Repeating Character Replacement
subtitle:  (Python, Java) 리트코드 - Longest Repeating Character Replacement
categories: algorithm
tags: leetcode
comments: true
# header-img:
---

[[문제 링크](https://leetcode.com/problems/longest-repeating-character-replacement/){:target="_blank"}]


## Python 풀이
```python
from collections import Counter

class Solution:
    def characterReplacement(self, s: str, k: int) -> int:
        start = 0
        end = 0
        n = len(s)
        counter = Counter()

        while end < n:
            counter[s[end]] += 1
            end += 1

            max_cnt = counter.most_common(1)[0][1]

            if end - start - max_cnt > k:
                counter[s[start]] -= 1
                start += 1

        return end - start
```
한번 최댓값이 된 상태에서는 start 값이 right값과 같이 1씩 올라가므로 최대 길이는 변화하지 않는다.

## Java 풀이
```java
import java.util.Collections;
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int characterReplacement(String s, int k) {
        int start = 0;
        int end = 0;
        Map<Character, Integer> counter = new HashMap<>();

        for (char letter : s.toCharArray()) {
            end += 1;
            counter.put(letter, counter.getOrDefault(letter, 0) + 1);
            Integer maxValue = Collections.max(counter.entrySet(), Map.Entry.comparingByValue()).getValue();

            if (end - start - maxValue > k) {
                counter.put(s.charAt(start), counter.get(s.charAt(start)) - 1);
                start += 1;
            }
        }
        return end - start;
    }
}
```

## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun characterReplacement(s: String, k: Int): Int {

        val accumulated = mutableMapOf<Char, Int>()
        var start = 0
        var answer = 0

        for ((idx, letter) in s.withIndex()) {
            accumulated[letter] = accumulated.getOrDefault(letter, 0) + 1

            val threshold = (idx - start + 1) - accumulated.values.max()
            if (threshold > k) {
                accumulated[s[start]] = accumulated.getOrDefault(s[start], 0) - 1
                start+=1
            } else {
                answer = max(answer, idx - start + 1)
            }
        }

        return answer
    }
}
```
