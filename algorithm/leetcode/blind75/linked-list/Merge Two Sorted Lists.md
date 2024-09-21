[문제 링크](https://leetcode.com/problems/merge-two-sorted-lists/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun mergeTwoLists(list1: ListNode?, list2: ListNode?): ListNode? {
        if (list1 == null) {
            return list2
        }

        if (list2 == null) {
            return list1
        }

        var one = list1
        var two = list2

        // head 지정
        val head = if (one!!.`val` <= two!!.`val`) {
            one = one.next
            list1
        } else {
            two = two.next
            list2
        }
        var current = head!!

        // 작은 것을 head에 연결하고 해당하는 변수에 다음 타켓을 넣는다.
        while (one != null && two != null) {
            if (one.`val` <= two.`val`) {
                current.next = one
                current = one
                one = one.next
            } else {
                current.next = two
                current = two
                two = two.next
            }
        }
        
        // 남아있는것 이어 붙이기
        if (one != null) {
            current.next = one
        }

        if (two != null) {
            current.next = two
        }

        return head
    }
}
```
