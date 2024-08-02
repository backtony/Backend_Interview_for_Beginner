[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12932)


## 풀이
```python
def solution(n):    
    return list(map(int,str(n)))[::-1]
```

## Java 풀이
```java

class Solution {
    public int[] solution(long n) {
        return new StringBuilder().append(n).reverse().chars().map(Character::getNumericValue).toArray();
    }
}
```
builder 인자로 string, char값만 줄 수 있지만 이후에 append에서는 이외 타입도 줄 수 있다.  
reverse는 역순으로 바꾸는 것이고 chars는 String을 char로 쪼개서 해당 char의 정수값 IntStream을 반환한다.  
예를 들어 foreach로 찍어보면 "A"는 65로 나온다.  
Character의 getNumbericValue 메서드는 숫자형 문자 char 또는 숫자형 문자의 정수값을 주면 숫자로 바꿔준다. (ex '1' -> 1)  


## kotlin 풀이
```kotlin
class Solution {
    fun solution(n: Long): IntArray {
        return n.toString().reversed()
            .toCharArray()
            .map { it.digitToInt() }
            .toIntArray()
    }
}
```
