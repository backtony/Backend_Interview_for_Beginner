[문제 링크](https://leetcode.com/problems/non-overlapping-intervals/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun eraseOverlapIntervals(intervals: Array<IntArray>): Int {
        // 종료 시간이 제일 작은 순으로 정렬
        intervals.sortWith(compareBy { it[1] })

        var answer = 0
        var prev = intervals[0]
        for (idx in 1..intervals.lastIndex) {
            // 겹치면 현재 것을 제거
            if (prev[1] > intervals[idx][0]) {
                answer++
            } else {
                // 겹치지 않는다면
                prev = intervals[idx]
            }
        }

        return answer
    }
}
```
