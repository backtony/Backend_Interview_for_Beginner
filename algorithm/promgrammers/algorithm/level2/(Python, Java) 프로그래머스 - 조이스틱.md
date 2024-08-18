[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42860)


## Python 풀이
```python
import sys
sys.setrecursionlimit(19 ** 6)

answer = int(1e9)

def solution(name):
    n = len(name)
    move = [0] * n
    for idx in range(n):
        move[idx] = min(ord(name[idx]) - ord('A'), ord('Z') - ord(name[idx]) + 1)

    dfs(move, 0, 0, n)

    return answer


def dfs(move, pos, tot, n):
    global answer

    # 현재 위치 처리
    tot += move[pos]
    move[pos] = 0

    # 모두 처리 한 경우
    if sum(move) == 0:
        answer = min(tot, answer)
        return

    # 왼쪽으로 
    left = pos
    left_cnt = 0
    while move[left] == 0:
        left = (left - 1 + n) % n
        left_cnt += 1
    prev = move[left]
    dfs(move, left, tot + left_cnt, n)
    move[left] = prev  # 원상 복구

    #  오른쪽으로
    right = pos
    right_cnt = 0
    while move[right] == 0:
        right = (right + 1) % n
        right_cnt += 1
    prev = move[right]
    dfs(move, right, tot + right_cnt, n)
    move[right] = prev  # 원상 복구
```


## Java 풀이
```java
import java.util.Arrays;

class Solution {
    int answer = Integer.MAX_VALUE;

    public int solution(String name) {
        int n = name.length();
        int[] move = new int[n];

        // 초기화
        for (int idx = 0; idx < n; idx++) {
            move[idx] = Math.min('Z' - name.charAt(idx) + 1, name.charAt(idx) - 'A');
        }

        dfs(move, 0, 0, n);

        return answer;
    }

    private void dfs(int[] move, int pos, int tot, int n) {
        tot += move[pos];
        move[pos] = 0;

        if (Arrays.stream(move).sum() == 0) {
            answer = Math.min(answer, tot);
            return;
        }

        // 오른쪽 이동
        int move_cnt = 0;
        int next = pos;

        while (move[next] == 0) {
            move_cnt += 1;
            next = (next + 1) % n;
        }
        int prev = move[next];
        dfs(move, next, tot + move_cnt, n);
        move[next] = prev;

        // 왼쪽 이동
        move_cnt = 0;
        next = pos;

        while (move[next] == 0) {
            move_cnt += 1;
            next = (next - 1 + n) % n;
        }
        prev = move[next];
        dfs(move, next, tot + move_cnt, n);
        move[next] = prev;

    }
}
```


## kotlin 풀이
```kotlin
import kotlin.math.min

class Solution {
    fun solution(name: String): Int {
        
        // 미리 해당 칸에서 얼마나 조이스틱을 돌려야하는지 계산
        val target = name.toMutableList().map {
            min(it - 'A', 'Z' - it + 1)
        }.toMutableList()

        return dfs(target, 0, 0)
    }

    fun dfs(target: MutableList<Int>,position: Int, tot: Int): Int {
        var answer = tot
        answer += target[position]
        target[position] = 0

        // 매칭 완료
        if (target.sum() == 0) {
            return answer
        }

        // 오른쪽 이동
        var newPosition = position
        var cnt = 0
        while(target[newPosition] == 0) {
            newPosition = (newPosition + 1) % target.size
            cnt++
        }
        var temp = target[newPosition]
        val right = dfs(target, newPosition, answer + cnt)
        target[newPosition] = temp

        // 왼쪽 이동
        newPosition = position
        cnt = 0
        while(target[newPosition] == 0) {
            newPosition = (newPosition -1 + target.size) % target.size
            cnt++
        }
        temp = target[newPosition]
        val left = dfs(target, newPosition, answer + cnt)
        target[newPosition] = temp
        
        // 오른쪽 이동과 왼쪽 이동 시 최소 값
        return min(left, right)
    }
}
```




