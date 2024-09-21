[문제 링크](https://leetcode.com/problems/jewels-and-stones/)


## Python 풀이
```python
class Solution:
    def numJewelsInStones(self, jewels: str, stones: str) -> int:
        jewel_store = set()
        for jewel in jewels:
            jewel_store.add(jewel)

        cnt = 0
        for stone in stones:
            if stone in jewel_store:
                cnt += 1

        return cnt

```

## Java 풀이
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int numJewelsInStones(String jewels, String stones) {
        Map<Character, Integer> counter = new HashMap<>();
        for (char stone : stones.toCharArray()) {
            Integer value = counter.getOrDefault(stone, 0);
            counter.put(stone, value + 1);
        }

        int count = 0;
        for (char jewel : jewels.toCharArray()) {
            count += counter.getOrDefault(jewel, 0);
        }
        return count;

    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun numJewelsInStones(jewels: String, stones: String): Int {
        val charStones = stones.toCharArray()
        return jewels.map { jewel ->
            charStones.count { it == jewel }
        }.sum()
    }
}
```
