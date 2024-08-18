[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/87946)


## Python 풀이
```python
from itertools import permutations


def solution(k, dungeons):
    answer = 0
    for permutation in permutations(dungeons, len(dungeons)):
        remain = k
        cnt = 0
        for dungeon in permutation:
            if remain < dungeon[0]:
                break
            remain -= dungeon[1]
            cnt += 1
        answer = max(answer, cnt)

    return answer
```

## Java 풀이
```java
class Solution {

    List<List<Dungeon>> permutationList = new ArrayList<>();
    LinkedList<Dungeon> temp = new LinkedList<>();

    public int solution(int k, int[][] dungeons) {

        int length = dungeons.length;
        boolean[] visited = new boolean[length];
        permutation(dungeons, length, length, visited);

        int answer = 0;
        for (List<Dungeon> dungeonList : permutationList) {
            int cnt = 0;
            int remain = k;
            for (Dungeon dungeon : dungeonList) {
                if (remain < dungeon.minimumCost)
                    break;
                remain -= dungeon.useCost;
                cnt++;
            }
            answer = Math.max(answer, cnt);
        }

        return answer;
    }

    private void permutation(int[][] dungeons, int n, int r, boolean[] visited) {
        if (r == 0) {
            permutationList.add(List.copyOf(temp));
            return;
        }

        for (int i = 0; i < n; i++) {
            if (visited[i] == false) {
                visited[i] = true;
                temp.add(new Dungeon(dungeons[i][0], dungeons[i][1]));
                permutation(dungeons, n, r - 1, visited);
                temp.pollLast();
                visited[i] = false;
            }
        }
    }

    private class Dungeon {
        int minimumCost;
        int useCost;

        public Dungeon(int minimumCost, int useCost) {
            this.minimumCost = minimumCost;
            this.useCost = useCost;
        }
    }
}
```

## kotlin 풀이
```kotlin
import kotlin.math.max

class Solution {
    fun solution(k: Int, dungeons: Array<IntArray>): Int {
        var answer: Int = -1


        val permutations = permutation(List(dungeons.size) { it }, dungeons.size)
        permutations.forEach permutations@{ dungeonPermutation ->
            var cnt = 0
            var current = k

            dungeonPermutation.forEach { dungeonNum ->
                val dungeon = dungeons[dungeonNum]
                if (dungeon.first() <= current) {
                    cnt++
                    current -= dungeon[1]
                } else {
                    answer = max(answer, cnt)
                    return@permutations
                }
            }
            answer = max(answer, cnt)
        }
        return answer
    }

    fun <T> permutation(arr: List<T>, r: Int): List<List<T>> {
        if (arr.size < r) {
            return emptyList()
        }

        val result = mutableListOf<List<T>>()

        fun permute(current: List<T>, remain: List<T>) {

            if (current.size == r) {
                result.add(current)
                return
            }
            for (index in 0..remain.lastIndex) {
                permute(current + remain[index], remain - remain[index])
            }
        }
        permute(listOf(), arr)
        return result
    }
}
```


