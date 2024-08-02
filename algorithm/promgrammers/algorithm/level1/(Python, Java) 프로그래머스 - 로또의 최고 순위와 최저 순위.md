

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/77484)


## Python 풀이
```python
def solution(lottos, win_nums):
    win = set(win_nums)
    answer = []
    blank = 0
    cnt = 0
    for lotto in lottos:
        if lotto in win:
            cnt += 1
        elif lotto == 0:
            blank += 1

    top = cnt + blank

    if top <= 1:
        answer.append(6)
    else:
        answer.append(7 - top)

    if cnt <= 1:
        answer.append(6)
    else:
        answer.append(7 - cnt)
    
    return answer
```

## Java 풀이
```java
import java.util.*;

class Solution {
    public int[] solution(int[] lottos, int[] win_nums) {
        int[] answer = new int[2];
        HashSet<Integer> myNum = new HashSet<>();
        int zero=0;
        int match=0;
        int maxRank;
        int minRank;

        for (int lotto : lottos) {
            if (lotto == 0){
                zero+=1;
            }
            else{
                myNum.add(lotto);
            }
        }

        for (int win_num : win_nums) {
            if (myNum.contains(win_num)){
                match+=1;
            }
        }

        maxRank = 7 - (match+zero);
        minRank = 7- match;
        if(maxRank>6)
            maxRank = 6;
        if (minRank >6)
            minRank = 6;

        answer[0] = maxRank;
        answer[1] = minRank;
        return answer;
    }

    public static void main(String[] args) {
        Solution s = new Solution();
        int[] lotto = {44, 1, 0, 0, 31, 25};
        int[] win = {31, 10, 45, 1, 6, 19};
        s.solution(lotto,win);
    }
}
```

## kotlin 풀이
```kotlin
class Solution {
    fun solution(lottos: IntArray, win_nums: IntArray): IntArray {
        var correctCnt = 0
        var zeroCnt = 0
        lottos.forEach { lotto ->
            if (lotto == 0) {
                zeroCnt += 1
                return@forEach
            }

            if (lotto in win_nums) {
                correctCnt += 1
            }
        }
        var max = rank(7 - (correctCnt + zeroCnt))
        var min = rank(7 - correctCnt)

        return listOf(max, min).toIntArray()
    }

    private fun rank(x: Int): Int {
        return if (x > 6) 6 else x
    }
}
```
