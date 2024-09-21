[문제 링크](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun removeNthFromEnd(head: ListNode?, n: Int): ListNode? {
        if (head?.next == null) return null

        // path 기록
        var root = head
        var current: ListNode? = head
        val path = mutableListOf<ListNode>()
        while (current != null) {
            path.add(current)
            current = current.next
        }

        val targetFrontIdx = path.size - n - 1
        val targetBackIdx = path.size - n + 1

        // 맨 앞에서 1개만 있는 케이스는 걸러냈으므로
        // 여기서부터는 무조건 2개 이상으로 앞쪽이 없거나 뒤쪽이 없는 경우만 고려
        // 앞쪽이 없는 경우
        if (targetFrontIdx < 0) {
            root = path[targetBackIdx]
            // 뒤쪽이 없는 경우
        } else if (targetBackIdx > path.lastIndex) {
            path[targetFrontIdx].next = null
        } else {
            path[targetFrontIdx].next = path[targetBackIdx]
        }

        return root
    }
}
```
