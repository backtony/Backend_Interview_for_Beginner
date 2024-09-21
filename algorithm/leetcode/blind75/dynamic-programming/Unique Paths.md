[문제 링크](https://leetcode.com/problems/unique-paths/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun uniquePaths(m: Int, n: Int): Int {

        // dp 초기화
        val map = MutableList(n) {MutableList(m) {0} }
        for (x in 0 until m) {
            map[0][x] = 1
        }
        for (y in 0 until n) {
            map[y][0] = 1
        }

        // dp 계산
        for (y in 1 until n) {
            for (x in 1 until m) {
                map[y][x] = map[y-1][x] + map[y][x-1]
            }
        }

        return map[n-1][m-1]
    }
}
```
