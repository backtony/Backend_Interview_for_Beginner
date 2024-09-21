[문제 링크](https://leetcode.com/problems/container-with-most-water/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max
import kotlin.math.min

class Solution {
    fun maxArea(height: IntArray): Int {

        var answer = 0
        var left = 0
        var right = height.lastIndex

        while(left < right) {

            val container = min(height[left], height[right]) * (right - left)
            answer = max(answer, container)

            if (height[left] < height[right]) {
                left++
            }else {
                right--
            }
        }

        return answer
    }
}
```
memo 문제인 줄 알았으나 해결책이 안보였다. 그렇다면 빠르게 다른 알고리즘을 고민해봐야한다. => 투 포인터
