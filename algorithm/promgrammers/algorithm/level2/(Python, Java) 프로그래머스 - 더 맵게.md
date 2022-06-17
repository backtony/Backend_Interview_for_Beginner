[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42626)


## Python 풀이
```python
import heapq

def solution(scoville, K):
    answer = 0

    heapq.heapify(scoville)
    foodCount = len(scoville)
    while foodCount > 1:
        food1 = heapq.heappop(scoville)
        food2 = heapq.heappop(scoville)
        heapq.heappush(scoville, food1 + (food2 * 2))
        foodCount -= 1
        answer += 1
        if scoville[0] >= K:
            return answer

    return -1
```
범위가 크기때문에 복잡도를 고려해야 한다.  
문제에서 세는 횟수를 요구하고 있으므로 세는 횟수는 계속 세야하고 그 과정을 단축시켜야 한다.  
넣고 정렬하고 넣고 정렬하는 과정을 줄일 수 있는데 이는 힙 자료구조를 사용하면 해결할 수 있다.  
처음에는 heap에 for문으로 차례로 넣었는데 __heapify 메서드__ 가 이를 해결해준다는 것을 알았다.  
__heapify는 인수로 들어온 리스트를 힙으로 만들어준다.__


## Java 풀이
```java
class Solution {
    public int solution(int[] scoville, int K) {
        int answer = 0;
        // 초기화
        PriorityQueue<Integer> scovilles = new PriorityQueue<>();
        for (int hot : scoville) {
            scovilles.add(hot);
        }

        while (scovilles.size() != 1) {
            Integer lowestScore = scovilles.poll();
            if (lowestScore >= K)
                break;
            answer++;
            scovilles.add(lowestScore + (scovilles.poll() * 2));
        }

        if (scovilles.size() == 1 && scovilles.poll() < K)
            answer = -1;

        return answer;
    }
}
```
파이썬에서 heap을 사용했다면 자바에서는 PriorityQueue 자료구조를 사용하면 된다.