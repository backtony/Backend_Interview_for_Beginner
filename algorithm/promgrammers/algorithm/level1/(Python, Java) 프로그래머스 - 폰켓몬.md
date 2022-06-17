[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/1845)


## Python 풀이
```python
def solution(nums):
    pickCount = len(nums) // 2
    length = len(set(nums))

    if pickCount<=length:
        answer = pickCount
    
    else:
        answer = length

    return answer
```

## Java 풀이
```java
import java.util.HashSet;
import java.util.Set;

class Solution {
    public int solution(int[] nums) {

        int target = nums.length /2;
        Set<Integer> store = new HashSet<>();

        for (int num : nums) {
            store.add(num);
        }

        int answer = store.size();
        if (answer >=target){
            return target;
        }
        return answer;
    }
}
```

## Java Stream 풀이
```java
import java.util.Arrays;
import java.util.stream.Collectors;

class Solution {
    public int solution(int[] nums) {

        return Arrays.stream(nums)
                .boxed() // int를 Integer 타입 박싱으로 전환
                .collect(Collectors.collectingAndThen(Collectors.toSet(),
                        Ponketmons -> Math.min(Ponketmons.size(), nums.length/2)
                ));
    }
}
```
