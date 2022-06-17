
## Counter
collections.Counter() 메소드는 iterable 객체 즉, list, dict, set, str, bytes, tuple, range와 같은 반복 가능한 객체의 요소를 카운트하여 각각의 빈도 값을 {요소:빈도} 형태인 __해쉬 테이블형태(카운터 객체)__ 로 반환한다.  
여기서 핵심은 Counter 객체는 연산을 제공한다.  
```python
from collections import Counter

a = Counter("abc")
print(a) # Counter({'a': 1, 'b': 1, 'c': 1}) 
b = Counter("bcd") 
print(b) # Counter({'b': 1, 'c': 1, 'd': 1})
c = a-b
print(c) # Counter({'a': 1})
d = list(c)
print(d) # ['a']
```
__Counter 객체를 리스트로 형변환 시 count 개수는 제거되고 key값만 나오게 된다.__  
<Br>

이외의 제공 메서드
```python
from collections import Counter

d = Counter(["hello","hi"])
print(d) # Counter({'hello': 1, 'hi': 1})
print(d.get("hello")) # hello 카운트 값 반환 - > 1

d = Counter("aaabbbcccdde")
print(d) # Counter({'a': 3, 'b': 3, 'c': 3, 'd': 2, 'e': 1})
d = Counter("aaabbbcccdde")
e = d.most_common(3) # 카운트 상위 3개 [(키,카운트),(키,카운트)] 리스트 튜플 원소 형태로 반환
print(e) # [('a', 3), ('b', 3), ('c', 3)]

d = Counter(a=4,b=2,c=-2)
print(d) # Counter({'a': 4, 'b': 2, 'c': -2})
e = list(d.elements()) # elements는 카운트 개수가 양수인 key를 개수만큼 이터레이터로 반환 -> 리스트 형번환 필요
print(e) ['a', 'a', 'a', 'a', 'b', 'b']

# key - value 형식으로 뽑아내기
d = Counter(["hello","hi"])
for data, cnt in d.items():
    print(data,cnt)
# hello 1
# hi 1
```
<br>

## 리스트 표현식
코드를 줄일 때 매우 유용하게 사용되는 것 같다.
```python
a = [x for x in range(10)] # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
b = [x for x in a if x % 2 == 0] # [0, 2, 4, 6, 8]
c = [10 if x % 2 == 0 else 0 for x in a] # [10, 0, 10, 0, 10, 0, 10, 0, 10, 0]
```
<br>

## enumerate
반복문 사용 시 몇 번째 반복문인지 확인이 필요할 수 있다.  
인덱스 번호와 컬렉션의 원소를 tuple형태로 반환한다.  
```python
a  = [1,2,3,4]
for data in enumerate(a):
    print(data)
#(0, 1)
#(1, 2)
#(2, 3)
#(3, 4)

for idx, data in enumerate(a):
    print(idx,data)
#0 1
#1 2
#2 3
#3 4
```

<br>

## map
map(function, iterable) 형식으로 첫 번째 매개변수로는 함수가 오고 두 번째 매개변수로는 반복 가능한 자료형(리스트, 튜플 등)이 온다.  
map은 두 번째 인자로 들어온 반복 가능한 자료형 (리스트나 튜플)을 첫 번째 인자로 들어온 함수의 인자로 하나씩 넣는 작업을 한다.  
map 함수의 반환 값은 map객체 이기 때문에 해당 자료형을 list 혹은 tuple로 형 변환시켜주어야 한다.  
```python
a = ["1","2","3","4"]
print(list(map(int,a)))
# [1, 2, 3, 4]

s = "try hello world"
" ".join(map(lambda x : ''.join([word.upper() if idx%2 == 0 else word.lower() for idx, word in enumerate(x)]),s.split(' ')))
```
마지막 코드는 다른 사람 풀이에서 봤던 코드인데 가독성은 떨어지는데 여러가지를 복합적으로 사용해서 공부하기는 괜찮은 코드라서 가져왔다.  
공백을 기준으로 s를 짤라 나온 리스트를 하나씩 map의 첫번째 함수에 넣는데 첫번째 함수를 람다식으로 사용했다.  
즉, 짤라 나온 리스트는 람다식 : 오른쪽에 있는 함수에 x로서 들어가게 된다.


<br>

## zip
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

# 리스트 표현식으로 zip 두번 사용하기
arr1 = [[1, 2], [3, 4]]
arr2 = [[4, 5], [6, 7]]
print([[a + b for a, b in zip(x, y)] for x, y in zip(arr1, arr2)]) # [[5, 7], [9, 11]]
```
zip이 없었더라면 두개의 리스트를 같이 찍기 위해서는 range로 인덱스 값을 사용했을 것이다.  
위에서는 리스트 2개를 zip 인자로 주었고, zip은 각 인덱스끼리 튜플을 만들어 반복자를 반환했고 그것을 for문으로 받았다.  
zip은 unzip할때도 zip을 사용한다. 반복자이므로 인자에 *을 붙여 언팩해야 한다.  
주의해야할 점은 zip은 인자로 들어온 둘의 길이가 다르면 작은 길이를 기준으로 데이터를 엮고 나머지를 버린다.  

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
<br>

## rjust, ljust
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
<br>

## bin, oct, hex
```python
a = 10
print(bin(a)) # 0b1010
print(oct(a)) # 0o12
print(hex(a)) # 0xa
print(int(bin(a),2)) # 10
```
진수 변환 함수는 문자열로 반환된다.  
int는 인자와 진수를 주면 10진수로 변환시켜준다.
<br>

## 비트연산
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


<Br>


## Numpy
행렬 연산시 편리한 기능을 제공하는 라이브러리이다.
```python
import numpy

arr1 = [[1,2],[2,3]]
arr2 = 	[[3,4],[5,6]]

a1 = numpy.array(arr1) # 리스트를 행렬로 변환
print(a1)
# [[1 2]
#  [2 3]]
a2 = numpy.array(arr2) # 리스트를 행렬로 변환
print(a2)
# [[3 4]
#  [5 6]]
answer = a1 + a2 # 행렬 덧셈
print(answer)
# [[4 6]
#  [7 9]]
answer.tolist() # 리스트로 변환
print(answer.tolist()) # [[4, 6], [7, 9]]
```
곱셈, 덧셈, 나눗셈, 빼기 연산 등을 지원한다.
<Br>

## index
```python
a=[1,2,3,4]
print(a.index(2)) # 1
```
해당 값의 인덱스를 찾아서 반환한다.
