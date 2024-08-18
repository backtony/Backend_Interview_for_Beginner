[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42583)


## Python 풀이
```python
from collections import deque


def solution(bridge_length, weight, truck_weights):
    wait_truck = deque(truck_weights)
    bridge = deque([0] * bridge_length)

    cnt = 0
    bridge_weight = 0
    while wait_truck:
        cnt += 1
        bridge_weight -= bridge.popleft()

        if bridge_weight + wait_truck[0] <= weight:
            wait_truck_weight = wait_truck.popleft()
            bridge_weight += wait_truck_weight
            bridge.append(wait_truck_weight)
        else:
            bridge.append(0)

    while bridge_weight != 0:
        bridge_weight -= bridge.popleft()
        cnt += 1

    return cnt
```
이 풀이는 일일이 확인하기 때문에 길이가 1만 이하이기 때문에 가능한 풀이다.  
다리 길이만큼 일단 0으로 채워넣고 하나씩 내보내고 들어오고 하는 방식이다.  
들어올 수 있다면 트럭을 넣고 없다면 트럭을 대기시킨다.  
그러면서 시간을 카운트 한다.  


## Java 풀이
```java
import java.util.*;

class Solution {
    public int solution(int bridge_length, int weight, int[] truck_weights) {

        Queue<Integer> bridge = new LinkedList<>();
        for (int i = 0; i < bridge_length; i++) {
            bridge.add(0);
        }

        Queue<Integer> waitTrucks = new LinkedList<>();
        for (int truckWeight : truck_weights) {
            waitTrucks.add(truckWeight);
        }

        int currentWeight = 0;
        int cnt = 0;
        while (!waitTrucks.isEmpty()) {
            cnt += 1;
            currentWeight -= bridge.poll();

            if (currentWeight + waitTrucks.peek() <= weight) {
                Integer inTruck = waitTrucks.poll();
                currentWeight += inTruck;
                bridge.add(inTruck);
            } else {
                bridge.add(0);
            }
        }

        while (currentWeight != 0) {
            currentWeight -= bridge.poll();
            cnt += 1;
        }

        return cnt;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(bridge_length: Int, weight: Int, truck_weights: IntArray): Int {
        var cnt = 0

        // 다리 채우기
        val bridge = mutableListOf<Int>()
        repeat(bridge_length) {
            bridge.add(0)
        }

        truck_weights.forEach { truck ->

            // 진입 불가능한 경우
            while (weight < bridge.slice(1..bridge.lastIndex).sum() + truck) {
                cnt += 1

                bridge.removeFirst()
                bridge.add(0)
            }
            
            // 진입 가능한 경우
            cnt += 1
            bridge.removeFirst()
            bridge.add(truck)
        }
        
        // 마지막 차 빼기
        while(bridge.sum() != 0) {
            cnt += 1
            bridge.removeFirst()
        }

        return cnt
    }
}
```


