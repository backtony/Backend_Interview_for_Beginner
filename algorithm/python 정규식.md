

## 메타 문자
---
정규 표현식에 사용하는 메타 문자는 다음와 같다.
```
. ^ $ * + ? { } [ ] \ | ( )
```
정규 표현식에서 위의 문자들은 문자 자체의 의미가 아닌 특별한 용도로 사용된다.

<br>

## 문자 클래스 [ ]
---
문자 클래스 [ ]로 만들어진 정규식은 __[ ] 사이의 문자들과 매치__ 라는 의미를 갖는다.  
```python
[abc]

"a" # a가 있으므로 매치
"before" # b가 있으므로 매치
"dude" # a,b,c중 하나도 없으므로 매치 X
```
<br>

[ ] 안에 하이픈(-)을 사용하면 두 문자 사의의 범위(From - to)를 의미한다.
```python
[a-c] # [abc] 와 동일
[0-9] # [0123456789] 와 동일
[a-zA-z] # 알파벳 모두
```
<br>

문자 클래스 안에는 어떤 문자나 메타 문자도 사용할 수 있지만 ^를 주의해야 한다.  
^는 반대라는 의미를 갖는다.
```python
[^0-9] # 숫자가 아닌 문자와 매치
```
<br>

__자주 사용하는 문자 클래스__
```python
\d # [0-9]와 동일한 표현식
\D # [^0-9]와 동일한 표현식
\s # whitespace 문자와 매치 [ \t\n\r\f\v]와 동일한 표현식으로 맨 앞 빈칸은 공백을 의미
\S # whitespace가 아닌 것과 매치 [^ \t\n\r\f\v]와 동일
\w # 문자+숫자와 매치 [a-zA-z0-9_] 와 동일(특수문자는 포함 안되고 _언더바는 포함)
\W # 문자+숫자가 아닌 문자와 매치, [^a-zA-z0-9_] 와 동일
\b # 단어의 경계(공백)
```

<br>

## Dot(.)
---
정규 표현식에서 Dot(.)는 줄바꿈 문자인 \n 을 제외한 모든 문자와 매치된다.
```python
a.b # a + 모든문자 + b

aab # 매치
aob # 매치
abc # 매치 X
```
<Br>

문자 클래스 안에 있는 Dot은 문자 그대로의 Dot을 의미한다.
```python
a[.]b # a.b를 의미

a.b # 매치
acb # 매치 X
```
<Br>

## 반복(*)
---
반복(*)는 바로 앞에 있는 문자가 0부터 무한대로 반복할 수 있다는 의미다.
```python
ca*t

# 전부 매칭
ct
cat
caat
caaat
```
<br>

## 반복(+)
---
반복(*)와 달리 바로 앞에 있는 문자가 1부터 무한 반복할 수 있다.  
즉, 최소 횟수가 1번 이상이어야 된다는 점만 차이가 있다.
```python
ca+t

ct # 매칭 X
cat # 매칭
caat # 매칭
```
<br>

## 반복 횟수 제한{}
---
{m,n}을 통해 바로 앞의 값의 반복 횟수를 지정할 수 있다.
```python
ca{2}t # a는 반드시 2번 반복

cat # 매칭 X
caat # 매칭

ca{2,}t # a는 2번 이상 반복
cat # 매칭 X
caat # 매칭

ca{,2}t # 2번 이하로 반복
cat # 매칭
caat # 매칭
caaat # 매칭 X

ca{2,5}t # a는 2~5회 반복
cat # 매칭 X
caat # 매칭
caaaaat # 매칭
```
<br>

## ?
---
?는 {0,1}을 의미한다.
```python
ab?c # b는 있어도 되고 없어도 된다.

abc # 매칭
ac # 매칭
```
<br>

## 파이썬 정규식 re 모듈
---
파이썬에서 정규식을 지원하기 위해 re 모듈을 제공한다.
```python
import re

p = re.compile('ab*')
```
re.compile을 사용하여 정규 표현식을 컴파일한다.  
re.compile의 결과로 돌려주는 객체를 사용하여 이후 작업에 사용하면 된다.  

<br>

## 정규식을 이용한 문자열 검색
---

메서드|설명
---|---
match()|문자열의 처음부터 정규식과 매치되는지 조사한다.
search()|문자열 전체를 검색하여 정규식과 매치되는지 조사한다.
findall()|정규식과 매치되는 모든 문자열(substring)을 리스트로 돌려준다
finditer()|정규식과 매치되는 모든 문자열(substring)을 반복 가능한 객체로 돌려준다.
sub()|정규식과 매칭되는 문자를 치환해서 문자열로 돌려준다.
split()|정규식과 매칭되는 문자를 기준으로 잘라서 리스트로 돌려준다.

match, search는 정규식과 매치될 때는 match 객체를 돌려주고, 매치되지 않을 때는 None을 돌려준다.  
__코딩테스트에서 정규식을 사용한다면 보통 findall, split, sub를 사용하게 된다.__  

<br>

```python
import re
p = re.compile('[a-z]+')
```
위 패턴으로 예시를 보자.  
findall, split, sub는 보통 코딩테스트에서 자주 사용하니 위 컴파일버전 말고 축약버전으로 보자.  


### findall
```python
result = p.findall("life is too short")
print(result)
['life', 'is', 'too', 'short']

# 컴파일 없이 축약버전으로 
result = re.findall('[a-z]+',"life is too short")
```
정규식과 매치된 문자열을 list형식으로 반환한다.  

### sub
```python
# 축약 버전 sub(정규식,교체값,대상문자열)
answer = re.sub("[^a-z\d.\-_]", "", "h@ello")
```

### split
```python
# 축약 버전
result = re.split('\D',"100+60+30")
print(result)
['100', '60', '30']

result = re.split('(\D)',"100+60+30")
print(result)
['100', '+', '60', '+', '30']
```
괄호가 없으면 split의 기준이 되는 것들은 리스트에 포함되지 않고, 괄호가 있으면 기준이 되는 것들도 리스트에 포함된다.


### match
match 메서드는 문자열의 __처음부터__ 정규식과 매치되는지 조사한다.
```python
m = p.match('python')
print(m)
# <re.Match object; span=(0, 6), match='python'>
```
매치되므로 match 객체를 돌려준다.
```python
m = p.match("3 python")
print(m)
# None
```
처음 나오는 문자 3이 정규식에 부합하지 않아 None을 반환한다.  

### search
```python
m = p.search("python")
print(m)
# <re.Match object; span=(0, 6), match='python'>

m = p.search("3 python")
print(m)
# <re.Match object; span=(2, 8), match='python'>
```
첫 문자가 3이지만 search는 __처음부터 검색하는 것이 아니라 문자 전체를 검색하기__ 때문에 3 이후의 python과 매치된다.  



### finditer
```python
result = p.finditer("life is too short")
print(result)
#<callable_iterator object at 0x01F5E390>
```
findall에서 반환 되는 객체가 이터레이터로 온다.  
각 요소는 match 객체이다.  

### match 객체 메서드
앞서 match, search를 수행한 결과가 match 객체로 반환된다고 했다.  
match 객체는 다음과 같은 메서드를 제공한다.  

메서드|설명
---|---
group()|매치된 문자열을 돌려준다
start()|매치된 문자열의 시작 위치를 돌려준다
end()|매치된 문자열의 끝 위치를 돌려준다
span()|매치된 문자열의 (시작,끝)에 해당하는 튜플을 돌려준다

```python
m = p.match("python")

m.group() # 'python'
m.start() # 0
m.end() # 6
m.span() # (0, 6)

m = p.search("3 python")
m.group() # 'python'
m.start() # 2
m.end() # 8
m.span() # (2, 8)
```



<br>

## 컴파일 옵션
---
정규식을 컴파일 할 때 다음 옵션을 사용할 수 있다.
+ DOTALL : Dot(.)가 줄바꿈 문자를 포함하여 모든 문자와 매칭할 수 있도록 한다.
+ IGNORECASE : 대소문자와 관계없이 매치할 수 있도록 한다.
+ MULTILINE : 여루줄과 매치할 수 있도록 한다.
+ VERBOSE : verbose 모드를 사용할 수 있도록 한다.

### DOTALL
Dot(.)은 줄바꿈 문자(\n)를 제외한 모든 문자와 매치된다.  
줄바꿈 문자도 포함하고 싶다면 DOTALL 옵션을 사용한다.
```python
import re
p = re.compile('a.b')
m = p.match('a\nb')
print(m) #None

p = re.compile('a.b', re.DOTALL)
m = p.match('a\nb')
print(m)
# <re.Match object; span=(0, 3), match='a\nb'>
```

### IGNORECASE
```python
p = re.compile('[a-z]+', re.I)
p.match('python')
#<re.Match object; span=(0, 6), match='python'>
p.match('Python')
#<re.Match object; span=(0, 6), match='Python'>
p.match('PYTHON')
#<re.Match object; span=(0, 6), match='PYTHON'>
```
소문자만 의미하는 정규식이지만 I옵션으로 대소문자 관계없이 매칭시킬 수 있다.

### MUILTILINE
re.MULTILINE 또는 re.M 옵션은 메타 문자인 ^, $와 연관된 옵션이다.  
^는 문자열의 처음을 의미하고, $는 문자열의 마지막을 의미한다.  
예를 들어 정규식이 ^python인 경우 문자열의 처음은 항상 python으로 시작해야 매치되고, 만약 정규식이 python$이라면 문자열의 마지막은 항상 python으로 끝나야 매치된다는 의미이다.
```python
import re
p = re.compile("^python\s\w+")

data = """python one
life is too short
python two
you need python
python three"""

print(p.findall(data))
# ['python one']
```
정규식 ^python\s\w+은 python이라는 문자열로 시작하고 그 뒤에 whitespace, 그 뒤에 단어가 와야 한다는 의미이다.  
검색할 문자열 data는 여러 줄로 이루어져 있다.  
^ 메타 문자에 의해 python이라는 문자열을 사용한 첫 번째 줄만 매치된 것이다.
```python
import re
p = re.compile("^python\s\w+", re.MULTILINE)

data = """python one
life is too short
python two
you need python
python three"""

print(p.findall(data))
# ['python one', 'python two', 'python three']
```
re.MULTILINE 옵션으로 인해 ^ 메타 문자가 문자열 전체가 아닌 각 줄의 처음이라는 의미를 갖게 되었다.  

<br>

## 백슬래시 문제
---
정규 표현식을 사용할 때 혼란을 주는 요소로 백슬래시(\\)가 있다.  
```python
# 찾고자 하는 문자열 \section
\section # 정규식
```
정규식을 위에서 처럼 사용하면 \s 는 whitespace로 먹히기 때문에 의도한대로 매치가 이뤄지지 않는다.
```python
\\section
```
위 정규식에서 사용한 \가 문자 \임을 알려주기 위해서 백슬래시를 2개 사용하여 이스케이프 처리해야 한다.  
하지만 여기서 파이썬만의 문제가 있는데 파이썬 정규식 엔진에는 파이썬 문자열 리터럴 규칙에 따라 백슬래시 2개는 백슬래시 1개로 처리되어 전달된다.  
즉, 실제로 파이썬에서 사용하려면 다음과 같이 사용해야한다.
```python
p = re.compile('\\\\section')
```
위처럼 전달해야 최종적으로 백슬래시가 2개 있는 것이 된다.  
하지만 이는 매우 불편하여 Raw String임을 알려주는 파이썬 문법이 있다.
```python
p = re.compile(r'\\section')
```
정규식 문자열 앞에 r을 붙이면 Raw String 규칙에 의하여 백슬래시 1개는 백슬래시 2개를 사용한 것과 같은 의미를 갖게 된다.


