[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/86491)


## Python 풀이
```python
def solution(sizes):
    return max(max(x) for x in sizes) * max(min(x) for x in sizes)
```
나는 사실 위와는 다르게 풀었는데 위 코드가 너무 간단해서 이걸로 가져왔다.  
위 코드를 보면 문제를 풀때 첫 방향을 잘 잡아야 된다는 것을 느낀다.  

## Java 풀이
```java
class Solution {
    public int solution(int[][] sizes) {
        int x, y;
        x = y = 0;
        for (int[] size : sizes) {
            x = Math.max(Math.max(size[0], size[1]), x);
            y = Math.max(Math.min(size[0], size[1]), y);
        }
        return x * y;
    }
}
```