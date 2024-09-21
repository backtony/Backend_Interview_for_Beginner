[문제 링크](https://leetcode.com/problems/longest-palindromic-substring/)


## Python 풀이
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        length = len(s)

        def findPalindromic(left, right):
            while 0 <= left and right < length:
                if s[left] == s[right]:
                    left -= 1
                    right += 1
                else:
                    break

            return s[left + 1:right]

        if length == 1:
            return s

        answer = ""
        for idx in range(length):
            s1 = findPalindromic(idx, idx + 1)
            s2 = findPalindromic(idx, idx + 2)
            answer = max(answer, s1, s2, key=len)
        return answer
```

## Java 풀이
```java
class Solution {
    public String longestPalindrome(String s) {

        int length = s.length();
        if (length == 1)
            return s;

        String answer = "";
        for (int idx = 0; idx < length - 1; idx++) {
            String s1 = findPalindromic(s, idx, idx + 1);
            String s2 = findPalindromic(s, idx, idx + 2);
            String longestPalindromic = getLongestPalindromic(s1, s2);
            answer = getLongestPalindromic(longestPalindromic, answer);
        }
        return answer;
    }

    private String findPalindromic(String s, int left, int right) {
        while (0 <= left && right < s.length()) {
            if (s.charAt(left) == s.charAt(right)) {
                left--;
                right++;
            } else {
                break;
            }
        }
        return s.substring(left + 1, right);
    }


    private String getLongestPalindromic(String s1, String s2) {
        String longest = "";
        if (s1.length() <= s2.length()) {
            longest = s2;
        } else {
            longest = s1;
        }
        return longest;
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun longestPalindrome(s: String): String {

        var answer = ""
        for (start in 0..s.lastIndex) {
            val even = palindrome(s, start, start+1)
            val odd = palindrome(s, start, start+2)

            answer = listOf(even, odd, answer).maxBy { it.length }
        }

        return answer
    }

    fun palindrome(s: String, left: Int, right: Int): String {

        var newLeft = left
        var newRight = right
        var palindrome = s[0].toString() // 예외 케이스

        while (newLeft >= 0 && newRight <= s.lastIndex) {
            if (s[newLeft] == s[newRight]) {
                palindrome = s.substring(newLeft, newRight + 1)
                newLeft--
                newRight++
            } else {
                break
            }
        }

        return palindrome
    }
}
```
