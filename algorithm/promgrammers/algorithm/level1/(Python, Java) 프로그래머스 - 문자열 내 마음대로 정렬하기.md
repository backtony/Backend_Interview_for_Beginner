[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12915)


## Python 풀이
```python
def solution(strings, n):
    strings.sort(key=lambda x:(x[n],x))
    return strings
```

## Java 풀이
```java
class Solution {
    public String[] solution(String[] strings, int n) {
        Arrays.sort(strings, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                if (o1.charAt(n) == o2.charAt(n)) {
                    return o1.compareTo(o2);
                }
                return Character.compare(o1.charAt(n), o2.charAt(n));
            }
        });
        return strings;
    }
}
```