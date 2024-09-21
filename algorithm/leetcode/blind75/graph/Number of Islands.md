[문제 링크](https://leetcode.com/problems/number-of-islands/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun numIslands(grid: Array<CharArray>): Int {
        var answer = 0
        for (y in 0..grid.lastIndex) {
            for (x in 0..grid.first().lastIndex) {

                if (grid[y][x] == '1') {
                    answer += 1
                    dfs(grid, x, y)
                }
            }
        }

        return answer
    }

    private fun dfs(grid: Array<CharArray>, x: Int, y: Int) {
        grid[y][x] = '0'

        val bx = listOf(-1, 0, 1, 0)
        val by = listOf(0, 1, 0, -1)

        for (move in bx.zip(by)) {
            val px = x + move.first
            val py = y + move.second

            if (0 <= px && px <= grid[0].lastIndex && 0 <= py && py <= grid.lastIndex) {
                if (grid[py][px] == '1') {
                    dfs(grid, px, py)
                }
            }
        }
    }
}
```
