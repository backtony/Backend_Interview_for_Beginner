[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42746)


## Python 풀이
```python
def solution(numbers):
    class Predicate(str):
        def __lt__(self, other):
            return self + other < other + self # 오름차순 -> 작은 것을 앞쪽에

    result = ''.join(sorted(map(str, numbers), key=Predicate, reverse=True)) # 내림차순으로 정렬
    return "0" if result[0] == "0" else result
```


## Java 풀이
```java
class Solution {
    public String solution(int[] numbers) {
        List<String> arr = new ArrayList<>();
        for (int number : numbers) {
            arr.add(String.valueOf(number));
        }

        arr.sort(new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                return (o2 + o1).compareTo(o1 + o2);
            }
        });

        StringBuilder sb = new StringBuilder();
        for (String s : arr) {
            sb.append(s);
        }

        String answer = sb.toString();
        if (answer.charAt(0) == '0')
            return "0";
        return answer;
    }
}
```
두 숫자를 문자로 더해서 큰 경우를 우선적으로 정렬하는 방식이다.

## kotlin 풀이
```kotlin
class Solution {
    fun solution(numbers: IntArray): String {
        if (numbers.all { it == 0 }) return "0"

        return numbers.sortedWith(
            Comparator { o1, o2 ->
                // 1을 리턴하면 순서가 바뀐다.
                val first = (o1.toString() + o2.toString()).toInt()
                val second = (o2.toString() + o1.toString()).toInt()
                // compareTo는 호출자가 비교자보다 크면 1
                second.compareTo(first)
            }
        ).joinToString("")
    }
}
```
