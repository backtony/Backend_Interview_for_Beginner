[문제 링크](https://leetcode.com/problems/implement-trie-prefix-tree/description/)


## kotlin 풀이
```kotlin
import java.util.TreeSet

class Trie() {

    val set = TreeSet<String>()
    fun insert(word: String) {
        set.add(word)
    }

    fun search(word: String): Boolean {
        return set.contains(word)
    }

    fun startsWith(prefix: String): Boolean {
        return set.ceiling(prefix)?.startsWith(prefix) ?: false
    }

}
```
