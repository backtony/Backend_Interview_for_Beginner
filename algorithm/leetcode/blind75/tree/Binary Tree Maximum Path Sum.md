[문제 링크](https://leetcode.com/problems/binary-tree-maximum-path-sum/description/)


## kotlin 풀이
```kotlin
class Solution {
    var answer = Int.MIN_VALUE
    var head: TreeNode? = null

    fun maxPathSum(root: TreeNode?): Int {

        if (head == null) {
            head = root
        }

        if (root == null) return 0

        val left = maxPathSum(root.left)
        val right = maxPathSum(root.right)
        
        // 현재 root를 way로 잡았을때 result
        val currentWayResult = right + left + root.`val`
        // 현재 root를 지나가는 way로 잡았을 때 result
        val wayMaxResult = listOf(
            left + root.`val`,
            right + root.`val`,
            root.`val`,
        ).max()
        answer = listOf(wayMaxResult, answer, currentWayResult).max()

        return if (head == root) {
            answer
        } else {
            wayMaxResult
        }
    }
}
```
