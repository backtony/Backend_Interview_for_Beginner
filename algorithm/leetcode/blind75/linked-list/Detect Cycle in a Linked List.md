[문제 링크](https://leetcode.com/problems/linked-list-cycle/description/)

## kotlin 풀이
```kotlin
class Solution {
    fun hasCycle(head: ListNode?): Boolean {
        if (head == null) {
            return false
        }

        val visited = mutableSetOf<ListNode>()
        var current = head

        while (current?.next != null) {
            
            if (visited.add(current).not()) {
                return true
            }
            current = current.next
        }

        return false
    }
}
```
