[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/81301)


## Python 풀이
```python
def solution(s):
    answer = s
    words = ["zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"]
    cnt = [0] * 10

    for idx in range(10):
        cnt[idx] = s.count(words[idx])

    for idx in range(10):
        for _ in range(cnt[idx]):
            answer = answer.replace(words[idx], str(idx))

    return int(answer)
```

## Java 풀이
```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int solution(String s) {

        String[] numbers ={"zero","one","two","three","four","five","six","seven","eight","nine"};
        Map<String, String> map = new HashMap<>();
        int index =0;
        for (String number : numbers) {
            map.put(number,String.valueOf(index));
            index++;
        }

        for (String number : numbers) {
            s = s.replaceAll(number,map.get(number));
        }

        return Integer.valueOf(s);
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        System.out.println(solution.solution("one4seveneight"));
    }
}
```