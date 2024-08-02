[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/12935)


## Python 풀이
```python
def solution(arr):
    answer = arr
    answer.remove(min(arr))
    if len(answer) == 0:
        answer.append(-1)

    return answer
```

## Java 풀이
```java
class Solution {
    public int[] solution(int[] arr) {
        List<Integer> collect = Arrays.stream(arr).boxed().collect(Collectors.toList());
        Arrays.sort(arr);
        collect.remove(collect.indexOf(arr[0]));
        if (collect.size() == 0)
            return new int[]{-1};
        return collect.stream().mapToInt(Integer::intValue).toArray();
    }
}
```
배열을 List로 바꾸기 위해서는 stream으로 풀어주고 box 타입으로 변환시켜줘야 한다.  
바로 asList로 해버리면 int[]가 제네릭으로 들어가버린다. 

```java
class Solution {
    public int[] solution(int[] arr) {
        if (arr.length==1)
            return new int[]{-1};
        int min = Arrays.stream(arr).min().getAsInt();
        return Arrays.stream(arr).filter(num -> num != min).toArray();
    }
}
```

## kotlin
```kotlin
class Solution {
    fun solution(arr: IntArray): IntArray {
        if (arr.size == 1) {
            return listOf(-1).toIntArray()
        }
        val min = arr.minOrNull()
        return arr.filter { it != min }.toIntArray()
    }
}
```
