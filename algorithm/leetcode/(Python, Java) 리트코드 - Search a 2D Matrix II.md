[문제 링크](https://leetcode.com/problems/search-a-2d-matrix-ii/submissions/)


## Python 풀이
```python
from typing import List

class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        for row in matrix:
            if target in row:
                return True

        return False

```

## Java 풀이
```java
import java.util.Arrays;

class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {

        int length = matrix[0].length;
        for (int[] numbers : matrix) {
            for (int idx=0;idx<length;idx++){
                if(numbers[idx] == target)
                    return true;
            }
        }
        return false;
    }
}
```
