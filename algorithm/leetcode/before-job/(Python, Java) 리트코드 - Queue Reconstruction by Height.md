[문제 링크](https://leetcode.com/problems/queue-reconstruction-by-height/)


## Python 풀이
```python
from typing import List

import heapq

class Solution:
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
        q = []
        for person in people:
            heapq.heappush(q, (-person[0], person[1]))

        result = []
        while q:
            height, idx = heapq.heappop(q)
            result.insert(idx, [-height, idx])

        return result
```
키가 큰 순서대로 뽑는 최대 힙을 만들고 앞에 있는 키가 큰 사람 수를 인덱스로 취급해서 배열에 넣으면 된다.  
이유는 이미 앞선 배열에 들어 있는 것들은 무조건 자신보다 키가 큰 사람들이기 때문이다.  


## Java 풀이
```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
import java.util.PriorityQueue;

class Solution {
    public int[][] reconstructQueue(int[][] people) {
        PriorityQueue<Person> q = new PriorityQueue<>(new Comparator<Person>() {
            @Override
            public int compare(Person o1, Person o2) {
                int compare = Integer.compare(o2.height, o1.height);
                if (compare == 0) {
                    return Integer.compare(o1.tallerThanMe, o2.tallerThanMe);
                }
                return compare;
            }
        });

        for (int[] person : people) {
            q.add(new Person(person[0], person[1]));
        }

        List<int[]> answer = new ArrayList<>();
        while (!q.isEmpty()) {
            Person person = q.poll();
            int[] element = {person.height, person.tallerThanMe};
            answer.add(person.tallerThanMe, element);
        }

        return answer.toArray(new int[0][]);
    }

    private class Person {
        int height;
        int tallerThanMe;

        public Person(int height, int tallerThanMe) {
            this.height = height;
            this.tallerThanMe = tallerThanMe;
        }
    }
}
```

## kotlin 풀이
```shell
class Solution {
    fun reconstructQueue(people: Array<IntArray>): Array<IntArray> {

        val answer = mutableListOf<IntArray>()

        people.sortedWith(
            compareByDescending<IntArray> { it[0] }.thenBy { it[1] }
        ).forEach {
            answer.add(it[1], it)
        }
        
        return answer.toTypedArray()
    }
}
```
개수는 
