[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17686)


## Python 풀이
```python
import re

def solution(files):
    temp =[]
    for file in files:
        split = re.split('(\d+)', file)
        temp.append(split)
    temp.sort(key=lambda x:(x[0].lower(),int(x[1])))

    answer =[]
    for file in temp:
        answer.append(''.join(file))
    
    return answer
```

## Java 풀이
```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

class Solution {
    public String[] solution(String[] files) {

        Pattern pattern = Pattern.compile("([a-z\\s.-]+)([0-9]{1,5})");

        Arrays.sort(files, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                Matcher matcher1 = pattern.matcher(o1.toLowerCase());
                Matcher matcher2 = pattern.matcher(o2.toLowerCase());
                matcher1.find();
                matcher2.find();

                String header1 = matcher1.group(1);
                String header2 = matcher2.group(1);
                if (header1.equals(header2)) {
                    return Integer.compare(
                            Integer.parseInt(matcher1.group(2)),
                            Integer.parseInt(matcher2.group(2)));
                }
                return header1.compareTo(header2);
            }
        });

        return files;
    }

    public static void main(String[] args) {
        String[] files = {"img12.png", "img10.png", "img02.png", "img1.png", "IMG01.GIF", "img2.JPG"};
        Solution solution = new Solution();
        solution.solution(files);
    }
}
```
Pattern.compile로 정규식을 만들어내고 matcher의 인자로 input 값을 넣는다.  
find 메서드를 호출하면 패턴에 맞는 첫 번째 문자열을 찾아준다.  
group(0)은 전체 패턴을 의미하므로 1부터 시작하면 된다.  
그룹은 컴파일 패턴에서 ()로 묶어준 것을 그룹으로 칭한다.  
위 문제에서는 find를 그냥 찾는 용도로만 사용했지만 find메서드는 일치하는 문자열을 찾고 있다면 true를 반환한다.  
따라서 while 문에서 find를 호출해서 있는 경우 찾아오는 형식의 코딩이 가능하다.  

