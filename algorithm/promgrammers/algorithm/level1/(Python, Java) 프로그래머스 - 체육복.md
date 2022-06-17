[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42862)


## Python 풀이
```python
def solution(n, lost, reserve):
    # 여분 없이 잃어버린 학생
    lostStudent = [x for x in lost if x not in reserve]
    # 잃어버리지 않고 빌려줄 수 있는 학생
    reserveStudent = [x for x in reserve if x not in lost]

    answer = n - len(lostStudent)
    reserveStudent = set(reserveStudent)
    lostStudent.sort()

    for num in lostStudent:
        if num - 1 in reserveStudent:
            reserveStudent.remove(num - 1)
            answer += 1
        elif num + 1 in reserveStudent:
            reserveStudent.remove(num + 1)
            answer += 1

    return answer
```

## Java 풀이
```java
class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int answer = n;

        Set<Integer> reserveStudents = arrayToSet(reserve);
        Set<Integer> lostStudents = arrayToSet(lost);

        Set<Integer> intersection = lostStudents.stream()
                .filter(l -> reserveStudents.contains(l))
                .collect(Collectors.toSet());

        lostStudents.removeAll(intersection);
        reserveStudents.removeAll(intersection);

        for (Integer num : lostStudents) {
            if (reserveStudents.contains(num - 1)) {
                reserveStudents.remove(num - 1);
            } else if (reserveStudents.contains(num + 1)) {
                reserveStudents.remove(num + 1);
            } else {
                answer -= 1;
            }
        }

        return answer;
    }

    private Set<Integer> arrayToSet(int[] arr) {
        Set<Integer> set = new HashSet<>();
        for (int num : arr) {
            set.add(num);
        }
        return set;
    }
}
```