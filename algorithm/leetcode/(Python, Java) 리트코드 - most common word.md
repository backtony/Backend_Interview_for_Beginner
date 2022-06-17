[문제 링크](https://leetcode.com/problems/most-common-word/)


## Python 풀이
```python
from typing import List
import re
from collections import Counter

class Solution:
    def mostCommonWord(self, paragraph: str, banned: List[str]) -> str:
        words = [word for word in re.sub('[^\w]', ' ', paragraph).lower().split() if word not in banned]

        return Counter(words).most_common(1)[0][0]
```

## Java 풀이
```java
import java.util.*;

class Solution {
    public String mostCommonWord(String paragraph, String[] banned) {
        HashSet<String> bannedWords = new HashSet<>();
        for (String word : banned) {
            bannedWords.add(word);
        }

        String[] s = paragraph.toLowerCase().replaceAll("[^a-zA-Z]", " ").split("\\s+");
        HashMap<String, Integer> counterMap = new HashMap<>();
        for (String key : s) {
            if (bannedWords.contains(key))
                continue;
            Integer count = counterMap.getOrDefault(key, 0);
            counterMap.put(key,count+1);
        }        
        
        return Collections.max(counterMap.entrySet(),Map.Entry.comparingByValue()).getKey();
    }
}
```
자바에서 컬렉션 관련 기능이 필요할 때는 Collections를 찾아도록 하자.  
__마지막에 리턴문은 기억할 필요가 있다.__
