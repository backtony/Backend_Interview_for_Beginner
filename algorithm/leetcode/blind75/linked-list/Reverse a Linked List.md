[문제 링크](https://leetcode.com/problems/linked-list-cycle/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun reverseList(head: ListNode?): ListNode? {

        if (head == null) {
            return null
        }

        // prev, current, next를 변수로 뽑아서 사용한다.
        var prev: ListNode? = null
        var current = head
        var next: ListNode? = null

        while (current != null) {
            next = current.next
            current.next = prev
            prev = current
            current = next
        }

        return prev
    }
}
```
