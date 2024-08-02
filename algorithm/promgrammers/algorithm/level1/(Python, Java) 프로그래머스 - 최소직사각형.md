[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/86491)


## Python 풀이
```python
def solution(sizes):
    return max(max(x) for x in sizes) * max(min(x) for x in sizes)
```

## Java 풀이
```java
class Solution {
    public int solution(int[][] sizes) {
        int x, y;
        x = y = 0;
        for (int[] size : sizes) {
            x = Math.max(Math.max(size[0], size[1]), x);
            y = Math.max(Math.min(size[0], size[1]), y);
        }
        return x * y;
    }
}
```

## kotlin 풀이
```kotlin
import kotlin.math.max
import kotlin.math.min

class Solution {
    fun solution(sizes: Array<IntArray>): Int {
        val card = Card(0,0)

        sizes.forEach { size ->
            card.updateSize(size[0], size[1])
        }

        return card.size()
    }

    class Card(
        var x: Int,
        var y: Int,
    ) {
        fun size(): Int {
            return x.times(y)
        }

        fun updateSize(x: Int, y: Int) {
            this.x = max(max(x,y), this.x)
            this.y = max(min(x,y), this.y)
        }
    }
}
```
