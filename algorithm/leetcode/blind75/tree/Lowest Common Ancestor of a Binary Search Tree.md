[문제 링크](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun lowestCommonAncestor(root: TreeNode?, p: TreeNode?, q: TreeNode?): TreeNode? {

        if (root == null) return null

        val small = listOf(p,q).minBy { it!!.`val` }!!
        val big = listOf(p,q).maxBy { it!!.`val` }!!

        return when {
            big.`val` < root.`val` -> {lowestCommonAncestor(root.left,p,q)}
            small.`val` > root.`val` -> {lowestCommonAncestor(root.right,p,q)}
            else -> root
        }
    }
}
```

이진 탐색 트리(BST)의 특징은 왼쪽 자식은 부모보다 작고, 오른쪽 자식은 부모보다 크다.
