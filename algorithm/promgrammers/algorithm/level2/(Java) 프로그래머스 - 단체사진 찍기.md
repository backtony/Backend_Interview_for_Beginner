[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/1835?language=java)


## 풀이
```java
class Solution {

    static String[] character = {"A", "C", "F", "J", "M", "N", "R", "T"};
    static String[] result = new String[8];
    static boolean[] visited = new boolean[8];
    static int answer;

    public int solution(int n, String[] data) {
        answer = 0;
        permutation(0, data);
        return answer;
    }

    private void permutation(int idx, String[] data) {
        if (idx == 8) {
            StringBuilder sb = new StringBuilder();
            for (String s : result) {
                sb.append(s);
            }
            String target = sb.toString();

            for (String options : data) {
                int start = target.indexOf(options.charAt(0));
                int end = target.indexOf(options.charAt(2));
                int currentDistance = Math.abs(start - end) - 1;
                int conditionDistance = options.charAt(4) - '0';
                char operation = options.charAt(3);

                if (operation == '=' && currentDistance != conditionDistance)
                    return;

                if (operation == '>' && currentDistance <= conditionDistance)
                    return;

                if (operation == '<' && currentDistance >= conditionDistance)
                    return;
            }
            answer++;
            return;
        }

        for (int i = 0; i < 8; i++) {
            if (!visited[i]) {
                visited[i] = true;
                result[idx] = character[i];
                permutation(idx + 1, data);
                visited[i] = false;
            }
        }

    }

    public static void main(String[] args) {
        Solution solution = new Solution();
        String[] data = {"N~F=0", "R~T>2"};
        solution.solution(2, data);
    }
}
```
순열을 구해서 조건에 맞는 것만 카운트하면 된다.  
Python의 경우 itertools가 있지만 Java의 경우 직접 구해줘야 하는 부분이 불편하다.