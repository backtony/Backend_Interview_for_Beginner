[문제 링크](https://leetcode.com/problems/diameter-of-binary-tree/)


## Python 풀이
```python
class Solution:
    answer = 0

    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        def max_depth(root):
            if root is None:
                return 0

            left = max_depth(root.left)
            right = max_depth(root.right)
            self.answer = max(self.answer, left + right)

            return max(left, right) + 1

        max_depth(root)
        return self.answer

```
재할당이 필요하기 때문에 클래스에 answer 변수 선언하고 안에서는 self 로 참조한다.

## Java 풀이
```java


class Solution {
    int answer = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        maxDepth(root);
        return answer;

    }

    private int maxDepth(TreeNode root) {
        if (root == null)
            return 0;

        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        answer = Math.max(answer, left + right);
        return Math.max(left, right) + 1;
    }
}
```
