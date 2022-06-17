[문제 링크](https://leetcode.com/problems/group-anagrams/)


## 풀이
```python
from typing import List
from collections import defaultdict


class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        store = defaultdict(list)
        for str in strs:
            store[''.join(sorted(str))].append(str)
        return list(store.values())
```

## Java 풀이
```java
import java.util.*;
import java.util.stream.Collectors;

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, List<String>> anagramMap = new HashMap<>();

        for (String str : strs) {
            char[] chars = str.toCharArray();
            Arrays.sort(chars);
            String key = String.valueOf(chars);
            List<String> value = anagramMap.getOrDefault(key, new ArrayList<String>());
            value.add(str);
            anagramMap.put(key, value);
        }

        return new ArrayList<>(anagramMap.values());
        // return anagramMap.entrySet().parallelStream().map(Map.Entry::getValue)
        //         .collect(Collectors.toList());
    }
}
```