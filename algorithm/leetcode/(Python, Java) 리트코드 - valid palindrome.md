[문제 링크](https://leetcode.com/problems/valid-palindrome/)


## Python 풀이
```python
import re

class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = s.lower()
        s = re.sub('[^a-z0-9]', '', s)

        return s == s[::-1]
```

## Java 풀이
```java
class Solution {
    public boolean isPalindrome(String s) {
        s = s.toLowerCase().replaceAll("[^a-z0-9]", "");
        StringBuilder sb = new StringBuilder();
        String reverse = sb.append(s).reverse().toString();
        return s.equals(reverse);
    }
  
}
```