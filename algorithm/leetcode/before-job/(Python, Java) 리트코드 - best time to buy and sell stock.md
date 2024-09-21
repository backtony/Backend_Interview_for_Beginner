[문제 링크](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)


## Python 풀이
```python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        min_price = int(1e9)
        profit = 0

        for price in prices:
            min_price = min(min_price, price)
            profit = max(profit, price - min_price)

        return profit
```

## Java 풀이
```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        int minPrice = Integer.MAX_VALUE;

        for (int price : prices) {
            minPrice = Math.min(price, minPrice);
            profit = Math.max(price - minPrice, profit);
        }
        return profit;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {

        var min = prices[0]
        val result = MutableList(prices.size) { 0 }

        prices.forEachIndexed { index, price ->
            result[index] = price - min
            if (min > price) {
                min = price
            }
        }

        return result.max()
    }
}
```
