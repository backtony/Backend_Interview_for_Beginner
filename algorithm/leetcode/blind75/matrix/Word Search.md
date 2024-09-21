[문제 링크](https://leetcode.com/problems/word-search/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun exist(board: Array<CharArray>, word: String): Boolean {

        val positions = mutableListOf<Pair<Int, Int>>()
        // word 시작지점 추출
        for (y in 0..board.lastIndex) {
            for (x in 0..board[0].lastIndex) {
                if (board[y][x] == word[0]) {
                    positions.add(Pair(x, y))
                }
            }
        }

        for (position in positions) {
            val visited = MutableList(board.size) { MutableList(board[0].size) { false } }
            if (findWord(board, position,word, visited, "")) {
                return true
            }
        }

        return false
    }

    private fun findWord(
        board: Array<CharArray>,
        position: Pair<Int, Int>,
        word: String,
        visited: MutableList<MutableList<Boolean>>,
        found: String
    ): Boolean {
        val (x,y) = position
        visited[y][x] = true // 방문 처리
        var answer = found + board[y][x]

        // 찾으면 true
        if (answer == word) {
            return true
        }

        val directions = listOf(
            Pair(1,0),
            Pair(0,1),
            Pair(-1,0),
            Pair(0,-1),
        )

        // 맞으면 dfs
        for (direction in directions) {
            val px = x + direction.first
            val py = y + direction.second

            if (0<=px && px <= board[0].lastIndex && 0 <= py && py <= board.lastIndex) {
                if (visited[py][px] == false && board[py][px] == word[answer.length]) {
                    // 찾으면 true
                    val result = findWord(board, Pair(px, py), word, visited, answer)

                    // 찾은 경우
                    if (result) {
                        return true
                    } else {
                        // 못 찾은 경우, 방문 처리 해제
                        visited[py][px] = false
                    }
                }
            }
        }

        // 못찾으면 false
        return false
    }
}
```
여러 갈래로 같은 문자가 있는 위치가 있을 수 있으므로 bfs로는 풀지 못한다.
