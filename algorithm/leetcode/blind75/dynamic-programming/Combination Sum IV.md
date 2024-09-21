[문제 링크](https://leetcode.com/problems/combination-sum-iv/description/)


## kotlin 풀이
```kotlin
class Solution {
    fun combinationSum4(nums: IntArray, target: Int): Int {

        val memo = MutableList(target+1) {0}

        for (num in nums) {
            if (target >= num) {
                memo[num] = 1
            }
        }

        for (idx in 1..target) {

            for (num in nums) {
                val prev = idx - num
                if (prev >=1 && memo[prev] != Int.MAX_VALUE) {
                    memo[idx] += memo[prev]
                }
            }
        }

        return memo.last()
    }
}
```
중복순열 또는 dfs로 풀이할 경우 timeout 발생.
