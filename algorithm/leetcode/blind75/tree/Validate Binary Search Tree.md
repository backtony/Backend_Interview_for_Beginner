[문제 링크](https://leetcode.com/problems/validate-binary-search-tree/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun isValidBST(root: TreeNode?): Boolean {

        fun isValid(root: TreeNode?, min: Long, max: Long): Boolean {
            if (root == null) return true

            if (root.`val` <= min || root.`val` >= max) return false

            return isValid(root.left, min, root.`val`.toLong()) && isValid(root.right, root.`val`.toLong(), max)
        }

        if (root == null || (root.left == null && root.right == null)) return true

        return isValid(root, Long.MIN_VALUE, Long.MAX_VALUE)
    }
}
```
BST의 규칙은 왼쪽 노드의 최대값은 현재 노드보다 작아야하고 오른쪽 노드의 최솟값은 현재 노드보다 작아야한다.
