[문제 링크](https://leetcode.com/problems/maximum-depth-of-binary-tree/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun maxDepth(root: TreeNode?): Int {

        if (root == null) return 0


        val left = maxDepth(root.left)
        val right = maxDepth(root.right)

        return max(left, right) + 1

    }
}
```
