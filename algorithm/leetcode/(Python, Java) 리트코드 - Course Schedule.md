[문제 링크](https://leetcode.com/problems/course-schedule/)


## Python 풀이
```python
from typing import List

from collections import deque


class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:

        # 초기화
        in_cnt = [0] * numCourses
        course = [[] for _ in range(numCourses)]
        for main_course, pre_course in prerequisites:
            in_cnt[main_course] += 1
            course[pre_course].append(main_course)

        # 위상정렬 초기 세팅
        q = deque()
        for idx in range(numCourses):
            if in_cnt[idx] == 0:
                q.append(idx)

        # 위상정렬
        cnt = 0
        while q:
            cur_idx = q.popleft()

            for next_idx in course[cur_idx]:
                in_cnt[next_idx] -= 1
                if in_cnt[next_idx] == 0:
                    q.append(next_idx)

            cnt += 1

        if cnt == numCourses:
            return True
        return False
```

## Java 풀이
```java
import java.util.*;

class Solution {

    public boolean canFinish(int numCourses, int[][] prerequisites) {

        // 선수과목 초기화
        Map<Integer, List<Integer>> prerequisite = new HashMap<>();
        int[] in = new int[numCourses];
        for (int[] ints : prerequisites) {
            int mainCourse = ints[0];
            int preCourse = ints[1];
            List<Integer> value = prerequisite.getOrDefault(preCourse, new ArrayList<>());
            value.add(mainCourse);
            prerequisite.put(preCourse, value);
            in[mainCourse] += 1;
        }

        // 위상 정렬을 위한 작업 시작 //

        // in이 0인 것 큐에 담기
        Queue<Integer> q = new LinkedList<>();
        for (int idx = 0; idx < numCourses; idx++) {
            if (in[idx] == 0)
                q.add(idx);
        }

        int cnt = 0;
        while (!q.isEmpty()) {
            Integer idx = q.poll();
            List<Integer> nextCourse = prerequisite.getOrDefault(idx, new ArrayList<>());
            for (Integer course : nextCourse) {
                in[course] -= 1;
                if (in[course] == 0) {
                    q.add(course);
                }
            }
            cnt += 1;
        }
        
        // 모두 다 돌아서 끝난 경우에는 가능 
        if (cnt == numCourses)
            return true;
        
        return false;
    }
}
```
