[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12977)


## Python 풀이
```python
from itertools import combinations


def isDecimal(value):
    idx = 2
    end = value // 2
    while idx <= end:
        if value % idx == 0:
            return False
        idx += 1

    return True


def solution(nums):
    answer = 0
    for numbers in combinations(nums, 3):
        if isDecimal(sum(numbers)):
            answer += 1

    return answer
```

## Java 풀이
```java
import java.util.*;

class Solution {

    LinkedList<Integer> comb = new LinkedList<>();
    int[] numbers;
    int answer = 0;

    public int solution(int[] nums) {
        numbers = nums;
        combination(3, 0);

        return answer;
    }

    private void combination(int r, int target) {
        if (r == 0) {
            int sum = comb.stream().mapToInt(Integer::intValue).sum();
            if (isPrime(sum)) {
                answer += 1;
            }
            return;
        }
        if (target >= numbers.length) {
            return;
        } else {
            comb.add(numbers[target]);
            combination(r - 1, target + 1);

            comb.pollLast();
            combination(r, target + 1);
        }
    }

    private boolean isPrime(int x) {
        if (x == 1)
            return false;
        for (int i = 2; i < x; i++) {
            if (x % i == 0) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] ints = {1, 2, 3, 4};
        solution.solution(ints);
    }
}
```
개수만 더마면 되는 문제라 combination 함수에서 answer를 덧셈해줬다.  
만약 어려운 문제라면 combination을 구해서 후처리를 진행해줘야하는데 그럼 combination 함수에서 그 처리를 해야한다.  
그럼 함수 자체가 역할이 너무 많아지므로 combination은 조합을 만드는 일만 하도록 수정해서 아래 코드가 나왔다.  
```java
import java.util.*;

class Solution {

    LinkedList<Integer> tmp = new LinkedList<>();
    LinkedList<LinkedList<Integer>> comb = new LinkedList<>();
    int[] numbers;

    public int solution(int[] nums) {
        numbers = nums;

        combination(nums.length, 3, 0);
        return comb.size();
    }

    private void combination(int n, int r, int target) {
        if (r == 0) {
            int sum = tmp.stream().mapToInt(Integer::intValue).sum();
            if (isPrime(sum)) {
                comb.add((LinkedList<Integer>) tmp.clone());
            }
            return;
        }
        if (target >= n) {
            return;
        } else {
            tmp.add(numbers[target]);
            combination(n, r - 1, target + 1);

            tmp.pollLast();
            combination(n, r, target + 1);
        }
    }

    private boolean isPrime(int x) {
        if (x == 1)
            return false;
        for (int i = 2; i < x; i++) {
            if (x % i == 0) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] ints = {1, 2, 7, 6, 4};
        solution.solution(ints);
    }
}
```
python을 사용하면 조합, 순열을 라이브러리가 만들어줘서 편했는데 java는 제공되지 않아 조합 알고리즘을 익혀둘 필요가 있어 보인다.

## kotlin 풀이
```kotlin
import kotlin.math.sqrt

class Solution {
    fun solution(nums: IntArray): Int {
        var answer = 0

        for (i in 0..nums.lastIndex - 2) {
            for (j in i + 1..nums.lastIndex - 1) {
                for (k in j + 1..nums.lastIndex) {
                    val sum = nums[i] + nums[j] + nums[k]
                    if (isPrime(sum)) {
                        answer += 1
                    }
                }
            }
        }

        return answer
    }

    private fun isPrime(num: Int): Boolean {
        val sqrt = sqrt(num.toDouble())

        for (i in 2..sqrt.toInt()) {
            if (num % i == 0) {
                return false
            }
        }
        return true
    }
}
```
