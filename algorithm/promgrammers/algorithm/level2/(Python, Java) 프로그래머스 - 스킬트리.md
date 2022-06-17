[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/49993)


## Python 풀이
```python
from collections import deque


def solution(skill, skill_trees):
    cnt = 0
    for tree in skill_trees:
        skill_set = set(skill)
        q = deque(skill)

        key = 1
        for letter in tree:
            if letter in skill_set:
                if q[0] == letter:
                    skill_set.remove(q[0])
                    q.popleft()
                else:
                    key = 0
                    break

        if key:
            cnt += 1

    return cnt
```

## Java 풀이
```java
class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;

        for (String skillTree : skill_trees) {

            Set<Character> skillSet = new HashSet<>();
            Queue<Character> skillOrder = new LinkedList<>();
            for (char letter : skill.toCharArray()) {
                skillSet.add(letter);
                skillOrder.add(letter);
            }

            int key = 1;
            for (char order : skillTree.toCharArray()) {
                if (skillSet.contains(order)) {
                    if (skillOrder.peek() == order) {
                        skillSet.remove(skillOrder.poll());
                    } else {
                        key = 0;
                        break;
                    }
                }
            }
            if (key == 1)
                answer++;
        }

        return answer;
    }
}
```