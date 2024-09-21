[문제 링크](https://leetcode.com/problems/rotate-image/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun rotate(matrix: Array<IntArray>): Unit {
        // row의 element 순서 역전
        matrix.reverse()

        // 대각선 기준으로 역전
        for (y in 0..matrix.lastIndex) {
            for (x in y..matrix[0].lastIndex) {
                val temp = matrix[y][x]
                matrix[y][x] = matrix[x][y]
                matrix[x][y] = temp
            }
        }
    }
}
```
