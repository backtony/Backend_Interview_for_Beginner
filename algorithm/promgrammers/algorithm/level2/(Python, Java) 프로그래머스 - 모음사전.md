[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/84512)


## Python 풀이
```python
from itertools import product
from bisect import bisect_right


def solution(word):
    dictionary = []
    letters = ['A', 'E', 'I', 'O', 'U']
    for cnt in range(1, 6):
        for unit in product(letters, repeat=cnt):
            dictionary.append(''.join(unit))

    dictionary.sort()
    return bisect_right(dictionary, word)
```


## Java 풀이
```java
import java.util.ArrayList;
import java.util.List;

class Solution {

    List<String> dictionary = new ArrayList<>();
    String letters = "AEIOU";

    public int solution(String word) {
        dfs("", 0);
        return dictionary.indexOf(word); // ""가 한번 들어가기 때문에 +1 안해도 된다.
    }

    private void dfs(String str, int length) {

        if (length > 5)
            return;

        dictionary.add(str);

        for (int i = 0; i <= 4; i++) {
            dfs(str + letters.charAt(i), length + 1);
        }
    }
}
```
순열, 조합 문제를 풀 때 항상 LinkedList를 사용해서 빼거나 더해주는 형식을 많이 사용했는데 함수의 인자로 새로 만들어서 넣어주는 경우라면 간단하게 풀이할 수 있는 것 같다.  
시간 복잡도는 조금 넘어갈 지라도 코테에서 이정도는 허용이 되는 것 같으니 기억하도록 하자.

