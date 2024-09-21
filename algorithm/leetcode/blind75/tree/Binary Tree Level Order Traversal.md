[문제 링크](https://leetcode.com/problems/binary-tree-level-order-traversal/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun levelOrder(root: TreeNode?): List<List<Int>> {
        if(root == null) return emptyList()

        // size가 안맞으면 한쪽을 맞춰주기
        val left = levelOrder(root.left).toMutableList()
        val right = levelOrder(root.right).toMutableList()
        if (left.size > right.size) {
            right.addAll(List(left.size - right.size) { emptyList() })
        }
        if (right.size > left.size) {
            left.addAll(List(right.size - left.size) { emptyList() })
        }

        val result = left.zip(right).map {
            it.first + it.second
        }.toMutableList()

        result.add(0, listOf(root.`val`))

        return result
    }
}
```
