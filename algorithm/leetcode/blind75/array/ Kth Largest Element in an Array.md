[문제 링크](https://leetcode.com/problems/kth-largest-element-in-an-array/)

```kotlin
import java.util.PriorityQueue

class Solution {
    fun findKthLargest(nums: IntArray, k: Int): Int {
        val q = PriorityQueue<Int>()

        for (num in nums) {
            q.add(num)
            if (q.size > k) {
                q.poll()
            }
        }
        return q.poll()
    }
}
```

O(n * log k) 복잡도를 갖는다.

quick-sort의 경우 최소 O(N)이지만 최대 O(N^2)의 복잡도가 나오므로 위의 방식이 더 낫다.

sort후 뒷쪽 인덱스로 찾는 것은 O(n * log n) 방식이므로 위에 방식이 가장 낫지 않을까 싶다. 
