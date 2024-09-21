[문제 링크](https://leetcode.com/problems/course-schedule/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun canFinish(numCourses: Int, prerequisites: Array<IntArray>): Boolean {

        // 0을 수강하려면 1을 먼저 수강해야한다.
        val visited = MutableList(numCourses) {false}
        // 선수과목 : 해당 과뫅을 선수로 하는 강의목록
        val preCourses = mutableMapOf<Int, MutableList<Int>>()
        // 과목 : 해당 과목을 듣기 위해 들어야할 선수 과목
        val courses = mutableMapOf<Int, MutableList<Int>>()
        for (prerequisite in prerequisites) {
            val pre = prerequisite[1]
            val main = prerequisite[0]
            preCourses[pre] = preCourses.getOrDefault(pre, mutableListOf()).apply { add(main) }
            courses[main] = courses.getOrDefault(main, mutableListOf()).apply { add(pre) }
        }

        // 선수과목 없이 바로 수강 가능한 과목 추출
        val q = mutableListOf<Int>()
        for (idx in 0 until numCourses) {
            if (courses[idx] == null) {
                q.add(idx)
            }
        }

        while(q.isNotEmpty()) {
            val current = q.removeLast()
            visited[current] = true // 현재 코스 수강 처리

            // current를 선수과목으로 가지고 있던 목록들을 추출해서 선수과목을 제거
            for (preCourse in preCourses[current] ?: emptyList()) {
                courses[preCourse] = courses[preCourse]!!.apply { remove(current) }
                
                // 선수과목이 다 사라졌다면 큐에 추가
                if (courses[preCourse]!!.isEmpty()) {
                    q.add(preCourse)
                }
            }
        }

        return visited.all { it }
    }
}

```
