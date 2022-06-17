[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12901)


## Python 풀이
```python
def solution(a, b):
    days = ['THU', 'FRI', 'SAT', 'SUN', 'MON', 'TUE', 'WED']
    months = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]

    return days[(sum(months[:a - 1]) + b) % 7]
```

## Java 풀이
```java
class Solution {
    public String solution(int a, int b) {
        String[] days = {"FRI", "SAT", "SUN", "MON", "TUE", "WED", "THU"};
        int[] months = {31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};
        int day = 0;
        for (int i = 1; i < a; i++) {
            day += months[i - 1];
        }
        day += b - 1;

        return days[day % 7];
    }
}
```