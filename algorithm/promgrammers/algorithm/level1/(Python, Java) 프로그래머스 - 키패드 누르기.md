
[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/67256)


## Python 풀이
```python
def solution(numbers, hand):
    answer = ''
    # 패드 위치
    pad = [[3, 1]]
    for i in range(4):
        for j in range(3):
            pad.append([i, j])

    left = [3, 0]
    right = [3, 2]
    for number in numbers:
        if number in [1, 4, 7]:
            left = pad[number]
            answer += "L"
        elif number in [3, 6, 9]:
            right = pad[number]
            answer += "R"
        else:
            position = pad[number]
            leftDistance = abs(left[0] - position[0]) + abs(left[1] - position[1])
            rightDistance = abs(right[0] - position[0]) + abs(right[1] - position[1])

            if leftDistance < rightDistance or (leftDistance == rightDistance and hand == "left"):
                left = position
                answer += "L"
            else:
                right = position
                answer += "R"

    return answer
```

## Java 풀이
```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

class Solution {
    Integer[] leftSide = {1,4,7};
    Integer[] rightSide = {3,6,9};

    Pad leftFinger = new Pad(3, 0);
    Pad rightFinger = new Pad(3, 2);

    public String solution(int[] numbers, String hand) {
        String answer = "";

        List<Pad> padList = new ArrayList<>();
        padList.add(new Pad(3,1)); // 0

        // 패드 위치 초기화
        for (int i=0;i<3;i++){
            for (int j=0;j<3;j++){
                padList.add(new Pad(i,j));
            }
        }

        answer = pushNumber(numbers, hand,padList);

        return answer;
    }

    private String pushNumber(int[] numbers, String hand, List<Pad> padList) {
        String answer = "";
        for (int number : numbers) {
            if(Arrays.asList(leftSide).contains(number)){
                leftFinger = padList.get(number);
                answer +="L";
            }
            else if (Arrays.asList(rightSide).contains(number)){
                rightFinger = padList.get(number);
                answer +="R";
            }
            else{
                Pad target = padList.get(number);
                int leftDistance = target.getDistance(leftFinger);
                int rightDistance = target.getDistance(rightFinger);
                if (leftDistance >rightDistance || (leftDistance == rightDistance && hand.equals("right"))){
                    rightFinger = target;
                    answer +="R";
                }
                else{
                    leftFinger = target;
                    answer +="L";
                }
            }
        }
        return answer;
    }

    class Pad {
        private int x;
        private int y;

        public Pad(int x, int y) {
            this.x = x;
            this.y = y;
        }

        public int getDistance(Pad pad){
            return Math.abs(x-pad.x) + Math.abs(y-pad.y);
        }
    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        int[] numbers = {1, 3, 4, 5, 8, 2, 1, 4, 5, 9, 5};
        String hand = "right";
        System.out.println(solution.solution(numbers,hand));
    }
}
```

## kotlin 풀이
```kotlin
import kotlin.math.absoluteValue

class Solution {
    fun solution(numbers: IntArray, hand: String): String {
        var answer = ""
        val numPad = generateNumPad()
        val left = Pad(0, -3, "*")
        val right = Pad(-2, -3, "#")

        numbers.forEach { num ->
            val pad = numPad.first { it.value == num.toString() }


            val leftCnt = left.calculateDistance(pad)
            val rightCnt = right.calculateDistance(pad)
            val hand = calculateHand(leftCnt, rightCnt, hand, pad)
            moveHand(hand, left, pad, right)
            answer += hand
        }

        return answer
    }

    private fun moveHand(hand: String, left: Pad, pad: Pad, right: Pad) {
        if (hand == "L") {
            left.update(pad)
        } else {
            right.update(pad)
        }
    }

    private fun calculateHand(leftCnt: Int, rightCnt: Int, hand: String, pad: Pad): String {
        if(pad.value in listOf("1","4","7")) {
            return "L"
        }

        if(pad.value in listOf("3","6","9")) {
            return "R"
        }

        return if (leftCnt < rightCnt) {
            "L"
        } else if (leftCnt > rightCnt) {
            "R"
        } else {
            if (hand == "right") {
                "R"
            } else {
                "L"
            }
        }
    }

    private fun generateNumPad(): List<Pad> {
        var pads = mutableListOf<Pad>()
        for (y in 0..2) {
            for (x in 0..2) {
                pads.add(Pad(-x, -y, (x + y + (y * 2) + 1).toString()))
            }
        }
        pads.add(Pad(0, -3, "*"))
        pads.add(Pad(-1, -3, "0"))
        pads.add(Pad(-2, -3, "#"))
        return pads
    }

    class Pad(
        var x: Int,
        var y: Int,
        var value: String,
    ) {
        fun update(pad: Pad) {
            this.x = pad.x
            this.y = pad.y
            this.value = pad.value
        }

        fun calculateDistance(target: Pad): Int {
            return (target.y.absoluteValue - this.y.absoluteValue).absoluteValue + (target.x.absoluteValue - this.x.absoluteValue).absoluteValue
        }
    }
}
```
