[문제 링크](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun buildTree(preorder: IntArray, inorder: IntArray): TreeNode? {
        // preorder 배열을 가변 리스트로 변환하여 첫 번째 요소를 제거할 수 있게 만듦
        return buildHelper(preorder.toMutableList(), inorder)
    }

    private fun buildHelper(preorder: MutableList<Int>, inorder: IntArray): TreeNode? {
        if (inorder.isEmpty()) return null

        // 전위 순회 결과는 중위 순회 분할 인덱스
        val rootValue = preorder.removeAt(0)
        val index = inorder.indexOf(rootValue)

        // 중위 순회 결과 분할 정복
        val node = TreeNode(rootValue)
        node.left = buildHelper(preorder, inorder.sliceArray(0 until index))
        node.right = buildHelper(preorder, inorder.sliceArray(index + 1 until inorder.size))

        return node
    }
}
```
논리 문제라기보다는 공식 문제라고 볼 수 있다.
preorder의 첫번째 값은 항상 루트 노드의 값이고 해당 값을 inorder에서 찾아서 왼쪽 오른쪽으로 쪼개면 왼쪽 서브 트리, 오른쪽 서브 트리가 된다.
