[문제 링크](https://leetcode.com/problems/same-tree/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun isSameTree(p: TreeNode?, q: TreeNode?): Boolean {

        if (p == null && q == null) {
            return true
        }

        val isLeftSame = isSameTree(p?.left, q?.left)
        val isRightSame = isSameTree(p?.right, q?.right)

        return isLeftSame && isRightSame && p?.`val` == q?.`val`
    }
}
```
