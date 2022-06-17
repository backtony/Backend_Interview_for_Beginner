
[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/64061)


## Python 풀이
```python
def solution(board, moves):
    answer = 0
    bucket = []

    # 각 위치에 있는 인형 일자 배열로 채우기
    length = len(board)
    doll = [[] for _ in range(length + 1)]
    for i in range(length):
        for j in range(length):
            if board[j][i] != 0:
                doll[i + 1].append(board[j][i])
    
    for move in moves:
        if len(doll[move]) != 0:
            bucket.append(doll[move].pop(0))
            # 2개 이상 채워져 있을 때만 깨지는 작업
            if len(bucket) >= 2 and bucket[-1] == bucket[-2]:
                bucket = bucket[:-2]
                answer += 2

    return answer
```

## Java 풀이
```java
import java.util.*;

public class Solution {


    public int solution(int[][] board, int[] moves) {
        int ans = 0;
        Stack<Integer> stack = new Stack<>();
        List<Deque<Integer>> machine = new ArrayList<>();
        machine.add(new LinkedList<>()); // 0번 째 더미

        // list 초기화
        for (int y = 0; y < board[0].length; y++) {
            Deque<Integer> q = new LinkedList<>();
            for (int x = 0; x < board.length; x++) {
                if (board[x][y] != 0) {
                    q.add(board[x][y]);
                }
            }
            machine.add(q);
        }


        for (int move : moves) {
            Deque<Integer> q = machine.get(move);
            if (!q.isEmpty()) {
                Integer pick = q.pollFirst();
                if (!stack.isEmpty() && stack.peek() == pick) {
                    stack.pop();
                    ans += 2;
                } else {
                    stack.add(pick);
                }
            }
        }
        return ans;

    }

    public static void main(String[] args) {
        int[][] board = {% raw %} {{0, 0, 0, 0, 0}, {0, 0, 1, 0, 3}, {0, 2, 5, 0, 1}, {4, 2, 4, 4, 2}, {3, 5, 1, 3, 1}} {% endraw %};
        int[] moves = {1, 5, 3, 5, 1, 2, 1, 4};
        Solution solution = new Solution();
        int ans = solution.solution(board, moves);
        System.out.println(ans);
    }
}
```