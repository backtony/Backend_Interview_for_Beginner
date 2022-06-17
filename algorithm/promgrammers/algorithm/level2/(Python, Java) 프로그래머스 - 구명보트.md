[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42885)


## Python 풀이
```python
from collections import deque


def solution(people, limit):
    people.sort()
    people = deque(people)
    total = 0
    while people:
        right = people.pop()
        if people and people[0] + right <= limit:
            people.popleft()
        total += 1
    return total
```
정렬해놓고 가장 큰거와 가장 작은 것을 매칭시켜서 태우는 방식이다.  
문제에서 주의할 것이 보트는 최대 2명뿐이 못탄다고 명시되있는 것을 잘 봐야하는 문제다.




## Java 풀이
```java
import java.util.Arrays;
import java.util.LinkedList;

class Solution {
    public int solution(int[] people, int limit) {

        Arrays.sort(people);
        LinkedList<Integer> q = new LinkedList<>();
        for (int person : people) {
            q.add(person);
        }

        int count = 0;
        int curWeight = 0;
        while (!q.isEmpty()) {
            curWeight += q.pollLast();

            if (!q.isEmpty() && q.get(0) + curWeight <= limit) {
                q.pollFirst();
            }
            count += 1;
            curWeight = 0;
        }

        return count;
    }
}
```