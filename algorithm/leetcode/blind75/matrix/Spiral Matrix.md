[문제 링크](https://leetcode.com/problems/spiral-matrix/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun spiralOrder(matrix: Array<IntArray>): List<Int> {
        val answer = mutableListOf<Int>()

        val directions = listOf(
            Pair(1,0),
            Pair(0,1),
            Pair(-1,0),
            Pair(0,-1),
        )

        var x = 0
        var y = 0
        var direction = 0

        while(0 <= x && x <= matrix[0].lastIndex && 0 <= y && y<= matrix.lastIndex && matrix[y][x] != Int.MAX_VALUE) {
            answer.add(matrix[y][x])
            matrix[y][x] = Int.MAX_VALUE // 방문 처리
            val (bx,by) = directions[direction]
            var px = x + bx
            var py = y + by

            // 인덱스를 초과 시 direction을 바꾸고 이동
            if (px < 0 || px > matrix[0].lastIndex || py <0 || py > matrix.lastIndex) {
                direction = (direction + 1) % 4
                val (bx,by) = directions[direction]
                x += bx
                y += by
                continue
            }

            // 이미 방문했다면 direction 바꾸고 이동
            if (matrix[py][px] == Int.MAX_VALUE) {
                direction = (direction + 1) % 4
                val (bx,by) = directions[direction]
                px = x + bx
                py = y + by
            }

            x = px
            y = py

        }

        return answer
    }
}
```
