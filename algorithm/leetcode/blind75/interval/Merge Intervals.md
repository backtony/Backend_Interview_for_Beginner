[문제 링크](https://leetcode.com/problems/merge-intervals/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max
import kotlin.math.min

class Solution {
    fun merge(intervals: Array<IntArray>): Array<IntArray> {
        
        if (intervals.size < 2) return intervals

        val result = mutableListOf<IntArray>()

        // 첫번째 인자로 정렬
        intervals.sortBy { it[0] }

        // 앞에 것이랑 비교해서 필요하면 병합하고 아니면 앞에 것 result에 추가
        var prev = intervals[0]
        for (idx in 1..intervals.lastIndex) {
            // 이전 것이랑 범위가 겹치면 병합
            if (prev[1] >= intervals[idx][0]) {
                prev = intArrayOf(min(prev[0], intervals[idx][0] ), max(prev[1], intervals[idx][1] ))
            } else {
                // 겹치지 않는다면 이전 것을 result에 추가하고 prev 변경
                result.add(prev)
                prev = intervals[idx]
            }
            
            // edge 케이스 : 마지막 인덱스의 경우 prev를 추가
            if (idx == intervals.lastIndex) {
                result.add(prev)
            }
        }

        return result.toTypedArray()
    }
}
```
