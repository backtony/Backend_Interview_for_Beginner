[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42587)


## Python 풀이
```python
from collections import deque


def solution(priorities, location):
    answer = 0
    q = deque()
    for idx, priority in enumerate(priorities):
        q.append((priority, idx))

    while q:
        priority, idx = q.popleft()
        if len(q) != 0 and priority < sorted(q)[-1][0]:
            q.append((priority, idx))
        else:
            answer += 1
            if idx == location:
                break

    return answer
```

## Python 풀이 2
```python
def solution(priorities, location):
    queue =  [(i,p) for i,p in enumerate(priorities)]
    answer = 0
    while True:
        cur = queue.pop(0)
        if any(cur[1] < q[1] for q in queue):
            queue.append(cur)
        else:
            answer += 1
            if cur[0] == location:
                return answer
```
다른 분의 풀이 중에 any를 사용한 것이 있어서 가져왔다.  
any는 모르는 내장 함수여서 배울 필요가 있었다.  


### any, all
+ any()
    - 인수 중 하나라도 True가 있으면 True  반환
+ all()
    - 인수 모두가 True 여야 True 반환

```python
>>> any([False, False, False])
False
>>> any([False, True, False])
True
>>> all([False, True, False])
False
>>> all([True, True, True])
True
```

## Java 풀이
```java
import java.util.LinkedList;

class Solution {
    public int solution(int[] priorities, int location) {
        int answer = 0;
        LinkedList<Print> prints = new LinkedList<>();

        for (int idx = 0; idx < priorities.length; idx++) {
            prints.add(new Print(priorities[idx], idx));
        }

        while (!prints.isEmpty()) {
            Print print = prints.pollFirst();
            if (prints.isEmpty()) {
                answer++;
                break;
            }

            Integer max = prints.parallelStream().map(Print::getPriority).max(Integer::compareTo).get();
            if (print.getPriority() < max) {
                prints.add(print);
            } else {
                answer++;
                if (print.getLocation() == location) {
                    break;
                }
            }

        }

        return answer;
    }

    class Print {
        int priority;
        int location;

        public Print(int priority, int location) {
            this.priority = priority;
            this.location = location;
        }

        public int getPriority() {
            return priority;
        }

        public int getLocation() {
            return location;
        }
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(priorities: IntArray, location: Int): Int {
        var answer = 0
        val temp = priorities.mapIndexed { index, i ->
            Pair(i, index)
        }.toMutableList()

        while(true) {
            val (prority, index) = temp.first()
            val maxPriority = temp.maxOf { it.first }
            if (prority == maxPriority) {
                answer++
                if (index == location) {
                    break
                }
                temp.removeFirst()
            } else {
                temp.add(temp.first())
                temp.removeFirst()
            }
        }

        return answer
    }
}
```
