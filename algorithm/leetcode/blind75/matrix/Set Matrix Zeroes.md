[문제 링크](https://leetcode.com/problems/set-matrix-zeroes/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun setZeroes(matrix: Array<IntArray>): Unit {

        val positions = mutableListOf<Pair<Int, Int>>()

        // get 0 position
        for (y in 0..matrix.lastIndex) {
            for (x in 0..matrix[0].lastIndex) {

                if (matrix[y][x] == 0) {
                    positions.add(Pair(x, y))
                }
            }
        }

        // make zero
        for (position in positions) {
            val (x,y) = position

            for (newY in 0..matrix.lastIndex) {
                matrix[newY][x] = 0
            }

            for (newX in 0..matrix[0].lastIndex) {
                matrix[y][newX] = 0
            }
        }
    }
}
```
