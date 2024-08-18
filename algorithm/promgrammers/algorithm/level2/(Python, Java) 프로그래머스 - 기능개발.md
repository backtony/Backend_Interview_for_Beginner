[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42586)


## 풀이
```python
import math


def solution(progresses, speeds):
    remainDay = []
    for progress, speed in zip(progresses, speeds):
        remain = math.ceil((100 - progress) / speed)
        if len(remainDay) == 0 or remainDay[-1][0] < remain:
            remainDay.append([remain, 1])
        else:
            remainDay[-1][1] += 1

    return [x[1] for x in remainDay]
```

## Java 풀이
```java
class Solution {
    public int[] solution(int[] progresses, int[] speeds) {
        List<Integer> answer = new ArrayList<>();

        // 큐 초기화
        Queue<Product> q = new LinkedList<>();
        for (int idx = 0; idx < progresses.length; idx++) {
            q.add(new Product(progresses[idx], speeds[idx]));
        }

        // deadLine 내에 수행할 수 있는지 검증
        int deadLine = q.poll().getDeadLine();
        int cnt = 1;
        while (!q.isEmpty()) {
            Product product = q.poll();
            if (product.canProgressInDeadLine(deadLine)) {
                cnt++;
            } else {
                answer.add(cnt);
                deadLine = product.getDeadLine();
                cnt = 1;
            }
        }
        answer.add(cnt);
        return answer.stream().mapToInt(Integer::intValue).toArray();
    }

    class Product {
        private int progress;
        private int speed;

        public Product(int progress, int speed) {
            this.progress = progress;
            this.speed = speed;
        }

        public int getDeadLine() {
            return (int) Math.ceil((100 - progress) / (double) speed);
        }

        public boolean canProgressInDeadLine(int deadLine) {
            return (100 - (progress + speed * deadLine)) <= 0 ? true : false;
        }
    }
}
```
이보다 더 숏코딩이 가능하겠지만 클래스를 사용해서 좀 더 우아한 코드를 작성하고 싶어서 클래스로 만들었다.


## kotlin 풀이
```kotlin
class Solution {
    fun solution(progresses: IntArray, speeds: IntArray): IntArray {
        val answer = mutableListOf<Int>()
        var release = 0

        progresses.zip(speeds).forEach {
            val progress = it.first
            val speed = it.second

            if ((progress + speed * release) >= 100) {
                answer[answer.lastIndex] += 1
                return@forEach
            }

            release = if ((100 - progress) % speed != 0) {
                ((100 - progress) / speed) + 1
            } else {
                (100 - progress) / speed
            }

            answer.add(1)
        }

        return answer.toIntArray()
    }
}
```
