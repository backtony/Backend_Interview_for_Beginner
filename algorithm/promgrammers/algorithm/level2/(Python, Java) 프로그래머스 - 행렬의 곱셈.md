[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12949?language=python3)


## Python 풀이 1
```python
def solution(arr1, arr2):
    y = len(arr2[0])
    x = len(arr1)
    ans = [[0] * y for _ in range(x)]

    for i in range(x):
        for j in range(y):
            tmp = 0
            for k in range(len(arr1[0])):
                tmp += arr1[i][k] * arr2[k][j]
            ans[i][j] = tmp

    return ans
```

## Python 풀이 2
```python
def solution(arr1, arr2):    
    return [[sum(a * b for a, b in zip(arr1_row, arr2_col)) for arr2_col in zip(*arr2)] for arr1_row in arr1]
```

## Java 풀이
```java
class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        int[][] answer = new int[arr1.length][arr2[0].length];

        for (int i = 0; i < arr1.length; i++) {
            for (int j = 0; j < arr2[0].length; j++) {
                for (int k = 0; k < arr1[0].length; k++) {
                    answer[i][j] += arr1[i][k] * arr2[k][j];
                }
            }
        }

        return answer;
    }
}
```