[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12905)


## Python 풀이
```python
def solution(board):
    height = len(board)
    weight = len(board[0])
    for x in range(1, height):
        for y in range(1, weight):
            if board[x][y] == 1:
                board[x][y] = min(board[x - 1][y - 1], board[x][y - 1], board[x - 1][y]) + 1

    answer = 0
    for x in range(height):
        temp = max(board[x])
        answer = max(answer, temp)

    return answer ** 2
```
일일이 찾아가면서 하게되면 4중 포문을 돌게 된다.  
최대 100만개의 좌표를 갖기 때문에 복잡도를 넘어선다.  
그렇다면 각각의 좌표에 만들 수 있는 정사각형의 최대를 담고 있도록 DP를 생각해내야 한다.  
dp는 자신의 위치에 만들 수 있는 최대 정사각형의 한 변의 길이로 설정한다.  
점화식은 자신을 기준 왼쪽, 위, 왼쪽 대각선 위 에서 가장 작은 길이를 갖는 것 +1이 현재 위치에서 만들 수 있는 가장 큰 정사각형의 길이다.  
답을 외우는건 의미가 없고 생각하는 흐름을 익혀야 한다.  
생각하는 흐름(DP??)이 1차적이고 그 후에 로직(DP점화식)을 생각해낼 수 있으면 된다. 


## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public int solution(int[][] board) {
        int weight = board[0].length;
        int height = board.length;

        for (int x = 1; x < height; x++) {
            for (int y = 1; y < weight; y++) {
                if (board[x][y] == 1) {
                    board[x][y] = Math.min(Math.min(board[x - 1][y - 1], board[x - 1][y]), board[x][y - 1]) + 1;
                }
            }
        }

        int max = 0;
        for (int x = 0; x < height; x++) {
            max = Math.max(Arrays.stream(board[x]).max().getAsInt(), max);
        }

        return max * max;
    }
}
```