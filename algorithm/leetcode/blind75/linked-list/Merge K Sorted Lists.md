[문제 링크](https://leetcode.com/problems/merge-k-sorted-lists/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun mergeKLists(lists: Array<ListNode?>): ListNode? {

        // q 삽입
        val q = PriorityQueue<ListNode>(compareBy { it.`val` })
        for (list in lists) {
            if (list != null) {
                q.add(list)
            }
        }

        var head : ListNode? = null
        var currnet : ListNode? = null
        while(q.isNotEmpty()) {
            val node = q.poll()
            val newNode = ListNode(node.`val`)

            if (head == null) {
                head = newNode
                currnet = newNode
            } else {
                currnet!!.next = newNode
                currnet = newNode
            }

            if (node.next != null) {
                q.add(node.next)
            }
        }

        return head
    }
}
```
