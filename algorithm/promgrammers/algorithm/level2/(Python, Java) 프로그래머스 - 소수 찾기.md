[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42839)


## Python 풀이
```python
import math
from itertools import permutations

def solution(numbers):
    answer = 0
    length = len(numbers)
    targets = set()

    for cnt in range(1, length + 1):
        targets |= set(map(int, map(''.join, set(permutations(numbers, cnt)))))

    for target in targets:
        if isPrime(target):
            answer += 1

    return answer


def isPrime(num):
    if num in [0, 1]:
        return False

    for i in range(2, int(math.sqrt(num)) + 1):
        if num % i == 0:
            return False
    return True
```


## Java 풀이
```java
class Solution {

    HashSet<Integer> done = new HashSet<>();
    LinkedList<Character> result = new LinkedList<>();
    boolean[] visited;
    int answer;

    public int solution(String numbers) {
        answer = 0;
        int length = numbers.length();
        for (int i = 1; i <= length; i++) {
            visited = new boolean[length];
            result.clear();
            permutation(numbers, length, i);
        }

        return answer;
    }

    private void permutation(String numbers, int n, int c) {
        if (c == 0) {
            StringBuilder sb = new StringBuilder();
            for (Character character : result) {
                sb.append(character);
            }
            int number = Integer.parseInt(sb.toString());
            
            // number 구하는 과정을 이렇게 짧게 stream으로 처리할 수 있으나 시작이 오래 걸린다.
            //  int number = Integer.parseInt(result.parallelStream()
            //         .map(String::valueOf)
            //         .collect(Collectors.joining()));

            if (isPrime(number) && !done.contains(number)) {
                answer += 1;
                done.add(number);
            }
            return;
        }

        for (int idx = 0; idx < n; idx++) {
            if (visited[idx] == false) {
                result.add(numbers.charAt(idx));
                visited[idx] = true;
                permutation(numbers, n, c - 1);
                result.pollLast();
                visited[idx] = false;
            }
        }
    }

    private boolean isPrime(int number) {
        if (number == 0 || number == 1)
            return false;

        for (int i = 2; i < (int) (Math.sqrt(number)) + 1; i++) {
            if (number % i == 0)
                return false;
        }
        return true;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(numbers: String): Int {
        val answer = mutableSetOf<Int>()

        for (cnt in 1..numbers.length) {
            permutation(numbers.toList(), cnt).forEach { candidate ->
                val num = candidate.joinToString("").toInt()

                if (isPrime(num)) {
                    answer.add(num)
                }
            }
        }

        return answer.size
    }

    fun isPrime(n: Int): Boolean {
        if (n == 1 || n == 0) {
            return false
        }
        val half = Math.sqrt(n.toDouble()).toInt()

        for (i in 2..half) {
            if (n % i == 0) {
                return false
            }
        }

        return true
    }

    fun <T> permutation(arr: List<T>, r: Int): List<List<T>> {
        val result = mutableListOf<List<T>>()

        fun permute(current: List<T>, remain: List<T>) {
            if (current.size == r) {
                result.add(current)
                return
            }

            for (idx in remain.indices) {
                permute(current + remain[idx], remain - remain[idx])
            }
        }

        permute(listOf(), arr)
        return result
    }
}
```

