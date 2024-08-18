[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/68936)


## Python 풀이
```python
def solution(arr):
    answer = [0, 0]

    def check(size, x, y):
        if size == 1:
            answer[arr[x][y]] += 1
            return

        target = arr[x][y]

        for px in range(size):
            for py in range(size):
                # 일치 하지 않으면 쪼개기
                if target != arr[x + px][y + py]:
                    resize = size // 2
                    check(resize, x, y)
                    check(resize, x + resize, y + resize)
                    check(resize, x + resize, y)
                    check(resize, x, y + resize)
                    return
        # 일치하면 해당에 +1
        answer[target] += 1

    check(len(arr), 0, 0)
    return answer
```

## Java 풀이
```java
class Solution {

    int[] answer;
    int[][] board;

    public int[] solution(int[][] arr) {
        answer = new int[2];
        board = arr;

        check(arr.length, 0, 0);
        return answer;
    }

    private void check(int size, int x, int y) {
        if (size == 1) {
            answer[board[x][y]] += 1;
            return;
        }

        int target = board[x][y];
        for (int dx = 0; dx < size; dx++) {
            for (int dy = 0; dy < size; dy++) {
                if (board[x + dx][y + dy] != target) {
                    int resize = size / 2;
                    check(resize, x, y);
                    check(resize, x + resize, y);
                    check(resize, x, y + resize);
                    check(resize, x + resize, y + resize);
                    return;
                }
            }
        }
        answer[target] += 1;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(arr: Array<IntArray>): IntArray {
        val answer: IntArray = intArrayOf(0,0)

        check(arr, arr.size, Pair(0,0), answer)

        return answer
    }

    fun check(arr: Array<IntArray>, size: Int, position: Pair<Int, Int>, answer: IntArray) {
        val currentX = position.first
        val currentY = position.second
        val target  = arr[currentX][currentY]

        if (size == 1) {
            answer[target] += 1
            return
        }

        for (x in 0 until size) {
            for (y in 0 until size) {
                if (target != arr[currentX+x][currentY+y]){
                    // 쪼개기
                    val half = size / 2
                    check(arr,half, Pair(currentX,currentY), answer)
                    check(arr,half, Pair(currentX+half,currentY), answer)
                    check(arr,half, Pair(currentX,currentY+half), answer)
                    check(arr,half, Pair(currentX+half,currentY+half), answer)
                    return
                }
            }
        }

        answer[target] += 1
    }
}
```
