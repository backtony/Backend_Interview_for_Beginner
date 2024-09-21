[문제 링크](https://leetcode.com/problems/reorder-list/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun reorderList(head: ListNode?): ListNode? {
        if (head?.next == null) return head

        // path 기록
        var current: ListNode? = head
        val path = mutableListOf<ListNode>()
        while (current != null) {
            path.add(current)
            current = current.next
        }

        val root = head
        current = head
        var left = 1
        var right = path.lastIndex
        var isLeftTurn = false

        while (left <= right) {
            var next: ListNode?
            if (isLeftTurn) {
                next = path[left]
                left++
                isLeftTurn = false
            } else {
                next = path[right]
                right--
                isLeftTurn = true
            }

            current!!.next = next
            current = next
            next.next = null
        }

        return root
    }
}
```
