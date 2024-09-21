[문제 링크](https://leetcode.com/problems/clone-graph/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun cloneGraph(node: Node?): Node? {
        val targetNode = node ?: return null
        val cloneNodes = mutableMapOf<Int, Node>()

        val newNode = Node(targetNode.`val`)
        cloneNodes.put(newNode.`val`, newNode)
        newNode.neighbors = cloneNeighbors(node.neighbors, cloneNodes)

        return newNode
    }

    private fun cloneNeighbors(neighbors: ArrayList<Node?>, cloneNodes: MutableMap<Int, Node>): ArrayList<Node?> {
        if (neighbors.isEmpty()) return ArrayList()

        val newNeighbors = ArrayList<Node?>()

        for (neighbor in neighbors) {
            if (neighbor == null) {
                newNeighbors.add(neighbor)
            } else {
                var newNode = cloneNodes[neighbor.`val`]
                
                // 이미 존재하지 않는 경우에만 새로 만들고, 이미 존재하면 해당 건은 복제하지 않고 그대로 사용하는 것이 핵심
                if (newNode == null) {
                    newNode = Node(neighbor.`val`)
                    cloneNodes.put(newNode.`val`, newNode)
                    newNode.neighbors = cloneNeighbors(neighbor.neighbors, cloneNodes)
                }
                
                newNeighbors.add(newNode)
            }
        }

        return newNeighbors
    }


    class Node(var `val`: Int) {
        var neighbors: ArrayList<Node?> = ArrayList<Node?>()
    }
}
```
