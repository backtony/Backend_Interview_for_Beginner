[문제 링크]()


## kotlin 풀이
```kotlin
class Solution {
    fun isSubtree(root: TreeNode?, subRoot: TreeNode?): Boolean {

        if (root == null) return false

        if (isSame(root, subRoot)) {
            return true
        }

        return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot)
    }

    fun isSame(mainNode: TreeNode?, subNode: TreeNode?): Boolean {

        if (mainNode == null && subNode == null) return true

        val isLeftSame = isSame(mainNode?.left, subNode?.left)
        val isRightSame = isSame(mainNode?.right, subNode?.right)

        return isLeftSame && isRightSame && mainNode?.`val` == subNode?.`val`
    }
}
```
