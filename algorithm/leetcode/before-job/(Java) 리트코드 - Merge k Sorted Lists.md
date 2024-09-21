[문제 링크](https://leetcode.com/problems/merge-k-sorted-lists/)



## Java 풀이
```java
import java.util.Comparator;
import java.util.PriorityQueue;

class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        ListNode result = new ListNode();
        ListNode temp = result;
        PriorityQueue<ListNode> q = new PriorityQueue<>(new Comparator<ListNode>() {
            @Override
            public int compare(ListNode o1, ListNode o2) {
                return Integer.compare(o1.val, o2.val);
            }
        });

        for (ListNode list : lists) {
            while (list != null) {
                q.add(list);
                list = list.next;
            }
        }
        
        while (!q.isEmpty()) {
            ListNode node = q.poll();
            temp.next = node;
            temp = temp.next;
        }
        temp.next = null;
        return result.next;
    }
}
```


## kotlin 풀이
```kotlin
class Solution {
    fun mergeKLists(lists: Array<ListNode?>): ListNode? {
        val q = PriorityQueue<ListNode>(compareBy { it.`val` })

        lists.forEach {
            var node = it
            while(node != null) {
                q.add(node)
                node = node.next
            }
        }

        val answer = ListNode(0)
        var temp = answer
        while(q.isNotEmpty()) {
            val poll = q.poll()
            temp.next = poll
            temp = poll
        }
        temp.next = null

        return answer.next
    }
}
```
