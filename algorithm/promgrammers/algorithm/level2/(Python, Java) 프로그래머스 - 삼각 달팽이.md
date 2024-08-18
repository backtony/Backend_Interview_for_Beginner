[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/68645)


## Python 풀이
```python
from itertools import chain


def solution(n):
    graph = [[0] * (x + 1) for x in range(n)]
    x, y = -1, 0  # 시작 좌표
    num = 1
    for i in range(n):  # 방향 0아래 ,1오른쪽,2 위
        for _ in range(i, n):  # 방향을 틀때마다 삽입 개수가 1개씩 줄어든다
            if i % 3 == 0:  # 아래
                x += 1
            elif i % 3 == 1:  # 오른쪽
                y += 1
            else:  # 상
                x -= 1
                y -= 1
            graph[x][y] = num
            num += 1

    return list(chain(*graph))
```
총 n번만큼 방향을 바꾸게 되고, 방향을 틀때마다 채워야하는 개수가 1개씩 줄어든다는 점을 이용하면 쉽게 풀 수 있다.


<Br>

itertools의 chain은 리스트를 합쳐주는 기능을 제공한다.  
```python
from itertools import chain

a = [[1,2,3],[4,5,6],[7,8,9]]

b = list(chain(*a))
print(b) # [1, 2, 3, 4, 5, 6, 7, 8, 9]

a = [1,2,3]
b = [4,5,6]
c = [7,8,9]
d = list(chain(a,b,c))
print(d) # [1, 2, 3, 4, 5, 6, 7, 8, 9]
```




## Java 풀이
```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int[] solution(int n) {
        int[][] graph = new int[n][];

        for (int i = 0; i < n; i++) {
            graph[i] = new int[i + 1];
        }

        int x = -1, y = 0;
        int num = 1;
        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                if (i % 3 == 0) {
                    x += 1;
                } else if (i % 3 == 1) {
                    y += 1;
                } else {
                    x -= 1;
                    y -= 1;
                }
                graph[x][y] = num;
                num += 1;
            }
        }

        List<Integer> answer = new ArrayList<>();
        for (int[] arr : graph) {
            for (int number : arr) {
                answer.add(number);
            }
        }

        return answer.parallelStream().mapToInt(Integer::intValue).toArray();
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(n: Int): IntArray {
        if (n == 1) {
            return intArrayOf(1)
        }
        val graph = mutableListOf<MutableList<Int>>()

        // 피라미드 채우기
        for (floor in 1..n) {
            graph.add(MutableList(floor) { Int.MAX_VALUE })
        }

        var x = 0
        var y = 0
        var direction = "D"
        var cnt = 1
        while (graph[y][x] == Int.MAX_VALUE) {
            graph[y][x] = cnt
            cnt++
            when (direction) {
                "D" -> {
                    if (y + 1 == n || graph[y + 1][x] != Int.MAX_VALUE) {
                        direction = "R"
                        x++
                    } else {
                        y++
                    }
                }

                "R" -> {
                    if (x + 1 > y || graph[y][x + 1] != Int.MAX_VALUE) {
                        direction = "U"
                        y--
                        x--
                    } else {
                        x++
                    }
                }

                "U" -> {
                    if (graph[y - 1][x - 1] != Int.MAX_VALUE) {
                        direction = "D"
                        y++
                    } else {
                        x--
                        y--
                    }
                }
            }
        }
        return graph.flatten().toIntArray()
    }
}
```
