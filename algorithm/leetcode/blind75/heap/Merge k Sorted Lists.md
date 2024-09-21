[문제 링크](https://leetcode.com/problems/merge-k-sorted-lists/description/)


## kotlin 풀이
```kotlin
import java.util.*

class Solution {
    fun mergeKLists(lists: Array<ListNode?>): ListNode? {

        if (lists.isEmpty()) return null

        var head: ListNode? = null
        var current: ListNode? = null
        val q = PriorityQueue<ListNode>(compareBy { it.`val` })
        for (list in lists) {
            if (list != null) {
                q.add(list)
            }
        }

        while (q.isNotEmpty()) {
            val node = q.poll()
            val newNode = ListNode(node.`val`)

            if (head == null) {
                head = newNode
                current = newNode

            } else {
                current!!.next = newNode
                current = newNode
            }

            if (node.next != null) {
                q.add(node.next)
            }

        }

        return head
    }
}
```
