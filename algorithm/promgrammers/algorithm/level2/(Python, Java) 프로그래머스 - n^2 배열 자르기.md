[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/87390)


## Python
```python
def solution(n, left, right):
    left_row = left // n
    right_row = right // n
    graph = []
    for row in range(left_row, right_row + 1):
        graph += [row + 1] * (row + 1) + [x for x in range(row + 2, n + 1)]

    length = right - left + 1
    left = left - n * left_row

    return graph[left:left + length]
```
left와 right 사이에 있는 row 배열을 만들고 뽑아냈다.  

## Java 풀이
```java
class Solution {
    public int[] solution(int n, long left, long right) {

        List<Long> graph = new ArrayList<>();
        long leftRow = left / n;
        long rightRow = right / n;
        for (long row = leftRow; row <= rightRow; row++) {
            for (long cnt = 0; cnt <= row; cnt++) {
                graph.add(row + 1);
            }

            for (long cnt = row + 1; cnt < n; cnt++) {
                graph.add(cnt + 1);
            }
        }

        int fromIndex = (int) (left % n);
        int toIndex = (int) (fromIndex + right - left + 1);
        return graph.subList(fromIndex, toIndex).parallelStream().mapToInt(Long::intValue).toArray();
    }
}
```