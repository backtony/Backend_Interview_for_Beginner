[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17677)


## Python 풀이
```python
from collections import Counter


def solution(str1, str2):
    token1 = [str1[idx - 1:idx + 1].upper() for idx in range(1, len(str1)) if str1[idx - 1:idx + 1].isalpha()]
    token2 = [str2[idx - 1:idx + 1].upper() for idx in range(1, len(str2)) if str2[idx - 1:idx + 1].isalpha()]

    counter1 = Counter(token1)
    counter2 = Counter(token2)

    intersection = set(token1) & set(token2)
    intersectionCount = sum([min(counter1.get(x), counter2.get(x)) for x in intersection])
    unionCount = len(token1) + len(token2) - intersectionCount

    if unionCount == 0:
        answer = 1
    else:
        answer = intersectionCount / unionCount

    return (int)(answer * 65536)
```


## Java 풀이
```java
class Solution {
    public int solution(String str1, String str2) {

        String word1 = str1.toLowerCase();
        String word2 = str2.toLowerCase();

        Map<String, Integer> wordMap1 = getGroup(word1);
        Map<String, Integer> wordMap2 = getGroup(word2);


        int intersectionCount = getIntersectionCount(word2, wordMap1, wordMap2);
        int unionCount = getUnionCount(wordMap1, wordMap2);

        if (unionCount == 0 && intersectionCount == 0)
            return 65536;

        return (int) ((double) intersectionCount / unionCount * 65536);
    }

    private Map<String, Integer> getGroup(String word) {
        Map<String, Integer> wordMap = new HashMap<>();

        for (int idx = 0; idx < word.length() - 1; idx++) {
            String key = word.substring(idx, idx + 2);


            if (!isAlpha(key))
                continue;

            if (wordMap.containsKey(key)) {
                wordMap.replace(key, wordMap.get(key) + 1);
            } else {
                wordMap.put(key, 1);
            }
        }
        return wordMap;
    }

    private boolean isAlpha(String key) {
        for (char ch : key.toCharArray()) {
            if (!Character.isAlphabetic(ch)) {
                return false;
            }
        }
        return true;
    }

    private int getIntersectionCount(String word2, Map<String, Integer> wordMap1, Map<String, Integer> wordMap2) {
        return wordMap1.entrySet().stream()
                .filter(entry -> word2.contains(entry.getKey()))
                .map(entry -> Math.min(wordMap1.get(entry.getKey()), wordMap2.get(entry.getKey())))
                .mapToInt(Integer::intValue)
                .sum();
    }

    private int getUnionCount(Map<String, Integer> wordMap1, Map<String, Integer> wordMap2) {
        Map<String, Integer> unionMap = new HashMap<>(wordMap2);
        for (String key : wordMap1.keySet()) {
            unionMap.put(key, Math.max(wordMap1.get(key), unionMap.getOrDefault(key, 0)));
        }
        
        return unionMap.entrySet().stream()
                .map(Map.Entry::getValue)
                .mapToInt(Integer::intValue)
                .sum();
    }
}
```


