[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12913)


## Python 풀이
```python
def solution(land):
    for i in range(1, len(land)):
        for j in range(4):
            land[i][j] = max(land[i - 1][: j] + land[i - 1][j + 1:]) + land[i][j]

    return max(land[-1])
```

## Java 풀이
```java
class Solution {
    int solution(int[][] land) {
        int length = land.length;
        for (int x = 1; x < length; x++) {
            for (int y = 0; y < 4; y++) {
                int temp = 0;
                for (int k = 0; k < 4; k++) {
                    if (k != y) {
                        temp = Math.max(temp, land[x - 1][k]);
                    }
                }
                land[x][y] += temp;
            }
        }

        return Arrays.stream(land[length - 1]).max().getAsInt();
    }
}
```