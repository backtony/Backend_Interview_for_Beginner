
[문제 링크](https://leetcode.com/problems/reverse-string/)


## Python 풀이
```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        s.reverse()
```

## Java 풀이
```java
class Solution {
    public void reverseString(char[] s) {
        int left = 0;
        int right = s.length - 1;
        while (left < right) {
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun reverseString(s: CharArray): Unit {
        s.reverse()
    }
}
```
