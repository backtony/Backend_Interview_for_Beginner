[문제 링크](https://leetcode.com/problems/subsets/)


## Python 풀이
```python
from typing import List
from itertools import combinations


class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:

        answer =[]
        for size in range(len(nums)+1):
            for comb in combinations(nums,size):
                answer.append(list(comb))

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

    public List<List<Integer>> subsets(int[] nums) {
        length = nums.length;
        for (int size = 0; size <= length; size++) {
            combination(nums, new LinkedList<>(), size, 0);
        }

        return answer;
    }

    private void combination(int[] nums, LinkedList<Integer> comb, int size, int idx) {
        if (size == 0) {
            answer.add(new ArrayList<>(comb));
            return;
        }

        if (idx >= length)
            return;

        comb.add(nums[idx]);
        combination(nums, comb, size - 1, idx + 1);

        comb.pollLast();
        combination(nums, comb, size, idx + 1);
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun subsets(nums: IntArray): List<List<Int>> {

        val result = mutableListOf<List<Int>>().apply { add(emptyList()) }
        for (num in 1..nums.size) {
            result.addAll(
                combination(nums.toList(), num)
            )
        }

        return result
    }

    fun <T> combination(arr: List<T>, r: Int): List<List<T>> {
        val result = mutableListOf<List<T>>()

        fun comb(current: List<T>, start: Int) {
            if (current.size == r) {
                result.add(current)
                return
            }

            for (next in start..arr.lastIndex) {
                comb(current + arr[next], next + 1)
            }
        }

        comb(listOf(), 0)

        return result
    }
}
```
