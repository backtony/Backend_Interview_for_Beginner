[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42889)


## Python 풀이
```python
from collections import Counter
from collections import deque


def solution(N, stages):
    result = []
    total = len(stages)
    q = deque()
    count = Counter(stages)
    for num in range(1, N + 1):
        nowStagePeople = count.get(num)
        if nowStagePeople is None:
            percent = 0
        else:
            percent = nowStagePeople / total
            total -= nowStagePeople

        q.append([percent, num])

    q = list(q)
    q.sort(key=lambda x: (-x[0], x[1]))

    for percent, num in q:
        result.append(num)

    return result
```
Counter.get에서 값이 존재하지 않는다면 0이 아니라 None이 나오는 것을 주의하자.  

## Java 풀이
```java
import java.util.Arrays;
import java.util.Comparator;

class Solution {
    public int[] solution(int N, int[] stages) {
        int peopleCount = stages.length;
        Stage[] stageArr = new Stage[N];
        int[] dpPeople = new int[N + 2];
        for (int i = 1; i <= N; i++) {
            stageArr[i - 1] = new Stage();
            stageArr[i - 1].setStageNum(i);
        }

        for (int stage : stages) {
            dpPeople[stage]++;
        }

        for (int i = 1; i <= N; i++) {
            double fail = 0;
            if (peopleCount != 0) {
                fail = (double) dpPeople[i] / peopleCount;
            }
            stageArr[i - 1].setFailPercent(fail);
            peopleCount -= dpPeople[i];
        }

        return Arrays.stream(stageArr)
                .sorted(Comparator.reverseOrder())
                .map(stage -> stage.getStageNum())
                .mapToInt(Integer::intValue).toArray();
    }

    class Stage implements Comparable<Stage> {
        int stageNum;
        double failPercent;

        public int getStageNum() {
            return stageNum;
        }

        public void setStageNum(int stageNum) {
            this.stageNum = stageNum;
        }

        public double getFailPercent() {
            return failPercent;
        }

        public void setFailPercent(double failPercent) {
            this.failPercent = failPercent;
        }

        @Override
        public int compareTo(Stage o) {
            return Double.compare(this.failPercent, o.getFailPercent());
        }
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(N: Int, stages: IntArray): IntArray {
        val stageUserCnt = stages.groupBy { it }.map { it.key to it.value.size }.toMap()
        val stageFailurePercent = calculatePercent(stageUserCnt, N)

        return stageFailurePercent.entries.sortedWith(
            compareByDescending<Map.Entry<Int, Double>> { it.value }.thenBy { it.key }
        ).map { it.key }.toIntArray()
    }

    private fun calculatePercent(
        stageUserCnt: Map<Int, Int>,
        stageCnt: Int,
    ): Map<Int, Double> {
        var stageFailurePercent = mutableMapOf<Int, Double>()
        var total = stageUserCnt.getOrDefault(stageCnt + 1, 0)

        for (stage in stageCnt downTo 1) {
            val currentStageUserCnt = stageUserCnt.getOrDefault(stage, 0)
            total += currentStageUserCnt
            var percent = 0.0
            if (total != 0) {
                percent = currentStageUserCnt.toDouble() / total
            }
            stageFailurePercent[stage] = percent
        }

        return stageFailurePercent
    }
}
```
