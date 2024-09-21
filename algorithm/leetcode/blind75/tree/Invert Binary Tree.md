[문제 링크](https://leetcode.com/problems/invert-binary-tree/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun invertTree(root: TreeNode?): TreeNode? {

        if (root == null) {
            return root
        }

        val left = invertTree(root.left)
        val right = invertTree(root.right)

        root.left = right
        root.right = left

        return root
    }
}
```
