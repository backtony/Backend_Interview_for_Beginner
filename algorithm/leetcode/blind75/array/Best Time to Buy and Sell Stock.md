[문제 링크](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)


## kotlin 풀이
```kotlin
import kotlin.math.max
import kotlin.math.min

class Solution {
    fun maxProfit(prices: IntArray): Int {

        var minPrice = prices[0]
        var profit = 0

        for (price in prices) {
            profit = max(profit, price - minPrice)
            minPrice = min(minPrice, price)
        }

        return profit
    }
}
```
