[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17679)


## Python 풀이
```python
# 1. 4개씩 묶인 지점을 찾아서 어딘가에 저장
# 2. 다 돌았으면 해당 지점을 -1로 변환
# 3. 다시 돌면서 -1인 지점은 자신의 행에서 위로 가면서 -1이 아닌 점을 찾아서 가져오고 해당 점을 -1로 바꾸고 그 위로 그 과정 반복

def solution(m, n, board):
    new_board = create_new_board(board)
    answer = 0
    spot = set()

    while True:
        # 4개로 묶인 곳 찾기
        find_pop_spot(m, n, new_board, spot)

        # 묶인 곳 지우기
        remove_pop_spot(new_board, spot)

        cnt = len(spot)
        if cnt == 0:
            break
        answer += cnt
        spot.clear()

        # 지워진 지점 채우기
        move_spot(m, n, new_board)

    return answer


def create_new_board(board):
    new_board = []
    for unit in board:
        new_board.append(list(unit))
    return new_board


def find_pop_spot(m, n, new_board, spot):
    for i in range(m - 1):
        for j in range(n - 1):

            if new_board[i][j] != -1:
                if new_board[i][j] == new_board[i + 1][j] == new_board[i][j + 1] == new_board[i + 1][j + 1]:
                    spot.add((i, j))
                    spot.add((i + 1, j))
                    spot.add((i, j + 1))
                    spot.add((i + 1, j + 1))


def remove_pop_spot(new_board, spot):
    for x, y in spot:
        new_board[x][y] = -1


def move_spot(m, n, new_board):
    for i in range(m - 1, 0, -1):
        for j in range(n):
            # 위로 올라가면서 전환
            if new_board[i][j] == -1:
                for k in range(i - 1, -1, -1):
                    if new_board[k][j] != -1:
                        new_board[i][j] = new_board[k][j]
                        new_board[k][j] = -1
                        break
```

## Java 풀이
```java
import java.util.HashSet;
import java.util.Objects;
import java.util.Set;

class Solution {
    public int solution(int m, int n, String[] board) {

        int answer = 0;
        char[][] newBoard = createNewBoard(m, n, board);

        while (true) {
            Set<Spot> spot = findPopSpot(m, n, newBoard);
            removeSpot(newBoard, spot);

            int cnt = spot.size();
            if (cnt == 0)
                break;
            answer += cnt;
            spot.clear();

            moveSpot(m, n, newBoard);
        }


        return answer;
    }


    private char[][] createNewBoard(int m, int n, String[] board) {
        char[][] newBoard = new char[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                newBoard[i][j] = board[i].charAt(j);
            }
        }
        return newBoard;
    }

    private Set<Spot> findPopSpot(int m, int n, char[][] newBoard) {
        Set<Spot> spot = new HashSet<>();
        for (int i = 0; i < m - 1; i++) {
            for (int j = 0; j < n - 1; j++) {
                if (newBoard[i][j] != '1') {
                    if (newBoard[i][j] == newBoard[i + 1][j] && newBoard[i][j] == newBoard[i][j + 1] && newBoard[i][j] == newBoard[i + 1][j + 1]) {
                        spot.add(new Spot(i, j));
                        spot.add(new Spot(i, j + 1));
                        spot.add(new Spot(i + 1, j));
                        spot.add(new Spot(i + 1, j + 1));
                    }
                }
            }
        }
        return spot;
    }

    private void removeSpot(char[][] newBoard, Set<Spot> spot) {
        for (Spot pop : spot) {
            newBoard[pop.x][pop.y] = '1';
        }
    }


    private void moveSpot(int m, int n, char[][] newBoard) {
        for (int i = m - 1; i >= 1; i--) {
            for (int j = 0; j < n; j++) {
                if (newBoard[i][j] == '1') {
                    for (int k = i - 1; k >= 0; k--) {
                        if (newBoard[k][j] != '1') {
                            newBoard[i][j] = newBoard[k][j];
                            newBoard[k][j] = '1';
                            break;
                        }
                    }
                }
            }
        }
    }

    private class Spot {
        int x;
        int y;

        public Spot(int x, int y) {
            this.x = x;
            this.y = y;
        }

        @Override
        public boolean equals(Object o) {
            if (this == o) return true;
            if (o == null || getClass() != o.getClass()) return false;
            Spot spot = (Spot) o;
            return x == spot.x && y == spot.y;
        }

        @Override
        public int hashCode() {
            return Objects.hash(x, y);
        }
    }
}
```


