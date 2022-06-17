[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/17681)


## Python 풀이
```python
def solution(n, arr1, arr2):
    answer = []

    for x,y in zip(arr1,arr2):
        secret = bin(x|y)[2:]
        secret = secret.rjust(n,"0")
        secret = secret.replace("1","#")
        secret = secret.replace("0", " ")
        answer.append(secret)

    return answer
```
이 문제를 통해 python의 내장 함수 몇가지를 알게 되어 정리하고자 한다.  

### zip
zip함수는 여러 개의 순회 가능한(iterable) 객체를 인자로 받고, 각 객체가 담고 있는 원소를 튜플의 형태로 차례로 접근할 수 있는 반복자(iterator)를 반환한다.  
설명은 조금 어렵지만 예시를 보면 아주 쉽게 이해할 수 있다.  

```python
a = [1,2,3]
b = [4,5,6,7,8]

for x in zip(a,b):
    print(x)
# (1, 4)
# (2, 5)
# (3, 6)


for x,y in zip(a,b):
    print(x,y)
# 1 4
# 2 5
# 3 6

c = zip(a,b)
print(c) # <zip object at 0x1059dec00>
print(*c) # (1, 4) (2, 5) (3, 6)


c = zip(a,b)
d,e = zip(*c)
print(d) # (1, 2, 3)
print(e) # (4, 5, 6)

```
zip이 없었더라면 두개의 리스트를 같이 찍기 위해서는 range로 인덱스 값을 사용했을 것이다.  
위에서는 리스트 2개를 zip 인자로 주었고, zip은 각 인덱스끼리 튜플을 만들어 반복자를 반환했고 그것을 for문으로 받았다.  
zip은 unzip할때도 zip을 사용한다. 반복자이므로 인자에 *을 붙여 언팩해야 한다.  
주의해야할 점은 zip은 인자로 들어온 둘의 길이가 다르면 작은 길이를 기준으로 데이터를 엮고 나머지를 버린다.  

### rjust, ljust
rjust는 오른쪽으로 정렬하고 빈공간에 원하는 문자열을 채운다.  
ljust는 왼쪽으로 정렬하고 빈공간에 원하는 문자열을 채운다.
```python
value = "100"
value = value.rjust(5,"0")
print(value) # 00100

value = "100"
value = value.ljust(5,"1")
print(value) # 10011
```

### bin, oct, hex
```python
a = 10
print(bin(a)) # 0b1010
print(oct(a)) # 0o12
print(hex(a)) # 0xa
print(int(bin(a),2)) # 10
```
진수 변환 함수는 문자열로 반환된다.  
int는 인자와 진수를 주면 10진수로 변환시켜준다.

### 비트연산
```python
a = 10 
b = 12 
print(bin(a)) # 0b1010
print(bin(b)) # 0b1100
print(a|b) # 14
print(a&b) # 8
print(bin(a&b)) # 0b1000
print(bin(a|b)) # 0b1110
```
10진수 값에 비트연산시 결과값이 10진수로 나온다.  


<br>

__cf) *의 역할__  
```python
# 곱셈 연산
print(1*5) # 5

# 언팩
a = [1,2,3,4,5]
print(*a) # 1 2 3 4 5

# 패킹
def _sum(*numbers):
    print(numbers) # (1,2,3,4,5)

_sum(1,2,3,4,5)

# 변수 할당
*a, b = [1,2,3,0.11]
print(a) # [1,2,3]
print(b) # 0.11
```


## Java 풀이
```java
class Solution {
    public String[] solution(int n, int[] arr1, int[] arr2) {
        String[] answer = new String[n];
        for (int i = 0; i < n; i++) {
            String binary = String.format("%16s",Integer.toBinaryString(arr1[i] | arr2[i]));
            binary = binary.substring(16-n);
            answer[i] = binary.replaceAll("0", " ").replaceAll("1", "#");
        }
        return answer;
    }
}
```
파이썬에는 rjust, ljust로 기존 문자열을 오른쪽, 왼쪽으로 밀고 남은 자리에 원하는 수를 넣을 수 있는 API가 있는데 Java는 그런게 없다.  
문제에서 16자리가 최대이므로 String.format으로 16자리를 찍으면 왼쪽에 빈 자리는 공백으로 채워지기 때문에 이를 이용해 풀이했다.  
참고로 format에 숫자 앞에 -를 붙이면 왼쪽 정렬된다.