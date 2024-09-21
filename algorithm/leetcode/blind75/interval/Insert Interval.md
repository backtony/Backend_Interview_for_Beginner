[문제 링크](https://leetcode.com/problems/insert-interval/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max
import kotlin.math.min

class Solution {
    fun insert(intervals: Array<IntArray>, newInterval: IntArray): Array<IntArray> {

        val result = mutableListOf<IntArray>()
        var idx = 0

        // add not need to merge
        while(idx < intervals.size && intervals[idx][1] < newInterval[0]) {
            result.add(intervals[idx])
            idx++
        }

        // merge
        var min = newInterval[0]
        var max = newInterval[1]
        while(idx < intervals.size && newInterval[1] >= intervals[idx][0]) {
            min = min(intervals[idx][0], min)
            max = max(intervals[idx][1], max)
            idx++
        }
        result.add(intArrayOf(min, max))


        // add extra
        while(idx < intervals.size) {
            result.add(intervals[idx])
            idx++
        }

        return result.toTypedArray()
    }
}
```
