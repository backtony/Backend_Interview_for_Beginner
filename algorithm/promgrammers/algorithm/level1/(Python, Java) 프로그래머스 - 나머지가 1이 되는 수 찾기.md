[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/87389)


## Python 풀이
```python
def solution(n):
    tmp = n - 1
    for i in range(2, n):
        if tmp % i == 0:
            return i
```

## Java 풀이
```java
class Solution {
    public int solution(int n) {
        int i=2;
        for (;i<n;i++){
            if (n%i==1)
                break;
        }
        return i;
    }
}
```