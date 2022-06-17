[문제 링크](https://leetcode.com/problems/combination-sum/)


## Python 풀이
```python
from typing import List


class Solution:

    def combinationSum(self, candidates: List[int], target: int) -> List[List[int]]:
        answer = []
        length = len(candidates)

        def dfs(sum, combination, idx):
            if sum == 0:
                answer.append(combination)
                return
            if sum < 0:
                return

            if idx >= length:
                return

            dfs(sum - candidates[idx], combination + [candidates[idx]], idx)
            dfs(sum, combination, idx + 1)

        dfs(target, [], 0)

        return answer
```

## Java 풀이
```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;

class Solution {

    List<List<Integer>> answer = new ArrayList<>();
    int length;

    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        length = candidates.length;
        combination(candidates, target, new LinkedList<>(), 0);
        return answer;
    }

    private void combination(int[] candidates, int target, LinkedList<Integer> comb, int idx) {
        if (target < 0)
            return;

        if (target == 0) {
            answer.add(new ArrayList<>(comb));
            return;
        }

        if (idx >= length)
            return;

        comb.add(candidates[idx]);
        combination(candidates, target - candidates[idx], comb, idx);

        comb.pollLast();
        combination(candidates, target, comb, idx + 1);
    }

    public static void main(String[] args) {
        int[] a = {2, 3, 6, 7};
        System.out.println(new Solution().combinationSum(a, 7));
    }
}
```
조합에서는 for문이 필요 없다는 것을 기억하자.