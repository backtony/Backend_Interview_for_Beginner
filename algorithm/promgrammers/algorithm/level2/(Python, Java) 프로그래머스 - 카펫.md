[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42842)


## Python 풀이
```python
import math

def solution(brown, yellow):
    tot = brown+yellow

    for height in range(1,int(math.sqrt(tot))+1):
        if tot%height == 0:
            weight = tot // height
            if ((weight-2) * (height-2)) == yellow:
                return [weight,height]
```




## Java 풀이
```java
class Solution {
    public int[] solution(int brown, int yellow) {
        int[] answer = new int[2];

        int tot = brown + yellow;

        for (int height = 1; height <= (int) Math.sqrt(tot); height++) {
            if (tot % height == 0) {
                int weight = tot / height;
                if (((weight - 2) * (height - 2)) == yellow) {
                    answer[0] = weight;
                    answer[1] = height;
                    break;
                }
            }
        }
        return answer;
    }
}
```
