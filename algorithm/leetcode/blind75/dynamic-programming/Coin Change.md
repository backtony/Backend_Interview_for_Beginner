[문제 링크](https://leetcode.com/problems/coin-change/)


## kotlin 풀이
```kotlin
import kotlin.math.min

class Solution {
    fun coinChange(coins: IntArray, amount: Int): Int {
        if (amount == 0) return 0
        
        val memo = MutableList(amount + 1) {Int.MAX_VALUE}
        coins.forEach {
            if (amount >= it) {
                memo[it] = 1
            }
        }

        for (target in 1..amount) {

            for (coin in coins) {
                val prev = target - coin
                if (prev > 0 && memo[prev] != Int.MAX_VALUE) {
                    memo[target] = min( memo[prev] + 1, memo[target])
                }
            }
        }

        if (memo[amount] == Int.MAX_VALUE) {
            return -1
        }

        return memo[amount]
    }
}
```
