[문제 링크](https://leetcode.com/problems/clone-graph/description/)


## kotlin 풀이
```kotlin
class Solution {

    fun cloneGraph(node: Node?): Node? {
        val newNodes = mutableMapOf<Int, Node>()
        return cloneNode(node, newNodes)
    }

    fun cloneNode(node: Node?, newNodes: MutableMap<Int,Node>): Node? {
        if (node == null) return null

        if (newNodes[node.`val`] != null) {
            return newNodes[node.`val`]
        }

        val newNode = Node(node.`val`)
        newNodes[node.`val`] = newNode
        
        val newNeighbours = ArrayList<Node?>()
        for (neighbor in node.neighbors) {
            newNeighbours.add(cloneNode(neighbor, newNodes))
        }
        newNode.neighbors = newNeighbours

        return newNode
    }
}
```
