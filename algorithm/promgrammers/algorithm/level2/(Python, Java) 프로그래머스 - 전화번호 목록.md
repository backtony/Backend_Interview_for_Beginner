[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42577)


## Python 풀이
```python
def solution(phone_book):
    token = set(phone_book)

    for numbers in phone_book:
        length = len(numbers)
        for idx in range(1, length):
            if numbers[:idx] in token:
                return False

    return True
```
100만 범위에 번호 길이가 20이므로 최대 2천만번의 연산으로 충분히 시간 안에 해결할 수 있다.



## Java 풀이
```java

class Solution {
    public boolean solution(String[] phone_book) {
        HashSet<String> set = new HashSet<>(List.of(phone_book));
        for (String number : phone_book) {
            for (int idx=1;idx<number.length();idx++){
                if(set.contains(number.substring(0,idx)))
                    return false;
            }
        }
        return true;
    }
}
```

