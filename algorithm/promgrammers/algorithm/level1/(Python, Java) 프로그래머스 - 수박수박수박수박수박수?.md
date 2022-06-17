[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12922)


## Python 풀이
```python
def solution(n):
    return "수박" * (n // 2) + "수" * (n % 2)
```

## Java 풀이
```java
class Solution {
    public String solution(int n) {
        StringBuilder sb = new StringBuilder();
        String word = "수박";
        for (int i=0;i<n/2;i++){
            sb.append(word);
        }
        if (n%2==1){
            sb.append("수");
        }
        return sb.toString();
    }
}
```