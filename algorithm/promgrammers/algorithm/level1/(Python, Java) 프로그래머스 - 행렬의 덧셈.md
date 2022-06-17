[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12950)


## Python 풀이
```python
def solution(arr1, arr2):
    row = len(arr1)
    column = len(arr1[0])
    answer = [[] for _ in range(row)]

    for i in range(row):
        for j in range(column):
            answer[i].append(arr1[i][j] + arr2[i][j])

    return answer
```

## Python 풀이 2
```python
import numpy

def solution(arr1, arr2):
    answer = numpy.array(arr1) + numpy.array(arr2)
    return answer.tolist()
```
numpy를 사용하면 행렬 연산을 쉽게 할 수 있다.

## Python 풀이 3
```python
def solution(arr1, arr2):
    return [[a + b for a, b in zip(x, y)] for x, y in zip(arr1, arr2)]
```
zip을 사용해도 간단하게 풀 수 있다.

## Java 풀이
```java
class Solution {
    public int[][] solution(int[][] arr1, int[][] arr2) {
        for (int i = 0; i < arr1.length; i++) {
            for (int j = 0; j < arr1[0].length; j++) {
                arr1[i][j] += arr2[i][j];
            }
        }
        return arr1;
    }
}
```