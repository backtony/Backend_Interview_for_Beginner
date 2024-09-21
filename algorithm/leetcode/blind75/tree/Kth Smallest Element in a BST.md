[문제 링크](https://leetcode.com/problems/kth-smallest-element-in-a-bst/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun kthSmallest(root: TreeNode?, k: Int): Int {

        if (root == null) return 0

        val leftCount = countNode(root.left)
        return when {
            leftCount + 1 == k -> root.`val`
            leftCount >= k -> kthSmallest(root.left, k)
            else -> kthSmallest(root.right, k - leftCount - 1)
        }
    }

    fun countNode(root: TreeNode?): Int {
        if (root == null) return 0

        return countNode(root.left) + countNode(root.right) + 1
    }
}
```
