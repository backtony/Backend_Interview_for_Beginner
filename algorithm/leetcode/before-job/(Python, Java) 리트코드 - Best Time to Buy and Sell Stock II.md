[문제 링크](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)


## Python 풀이
```python
from typing import List

class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        profit = 0
        for i in range(len(prices) - 1):
            if prices[i] < prices[i + 1]:
                profit += prices[i + 1] - prices[i]

        return profit

```

## Java 풀이
```java
class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0;
        for (int idx = 0; idx < prices.length - 1; idx++) {
            if (prices[idx] < prices[idx + 1]) {
                profit += prices[idx + 1] - prices[idx];
            }
        }
        return profit;
    }
}
```
다음날 이익이 난다면 파는 형식의 그리디 알고리즘이다.


## kotlin 풀이
```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {
        val q = mutableListOf<Int>()
        var answer = 0

        for (price in prices) {

            if (q.isEmpty()) {
                q.add(price)
                continue
            }

            if (q.last() <= price) {
                q.add(price)
                continue
            }

            if (q.size >= 2) {
                answer += q.last() - q.first()
            }

            q.clear()
            q.add(price)
        }
        
        if (q.isNotEmpty()) {
            answer += q.last() - q.first()
        }
        return answer
    }
}
```
