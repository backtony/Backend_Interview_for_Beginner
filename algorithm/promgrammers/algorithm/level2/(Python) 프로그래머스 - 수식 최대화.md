[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/67257)



## Python 풀이 1
```python
import re
from itertools import permutations


def solution(expression):
    operations = [x for x in ['*', '-', '+'] if x in expression]
    operations_permutation = permutations(operations, len(operations))
    split_expression = re.split('(\D)', expression)  # 정규식으로 자를 수도 있다 리스트로 반환해줌 괄호가 없으면 \D는 제거됨

    answer = []
    for operations in operations_permutation:
        copy_expression = split_expression[:]  # 복사
        for operation in operations:
            # 뽑은 operation 으로 연결된 숫자들 모두 연산해서 결과로 붙여준다.
            while operation in copy_expression:
                operation_idx = copy_expression.index(operation)
                result = str(eval(copy_expression[operation_idx - 1] + operation + copy_expression[operation_idx + 1]))
                copy_expression[operation_idx - 1] = result
                copy_expression = copy_expression[:operation_idx] + copy_expression[operation_idx + 2:]

        answer.append(abs(int(copy_expression[0])))

    return max(answer)
```
정규식 split을 사용하면 원하는 문자를 기준으로 잘라서 리스트로 반환해준다.  
괄호를 사용할 경우 자르는 문자도 리스트에 포함해주고 괄호를 사용하지 않는다면 자를 때 사용한 문자는 리스트에 포함되지 않는다.


## Python 풀이 2
```python
from itertools import permutations

def calc(priority, n, exp):
    if n == 2:
        return str(eval(exp))

    if priority[n] == '*':
        result = '*'.join([calc(priority, n + 1, x) for x in exp.split('*')])
    elif priority[n] == '+':
        result = '+'.join([calc(priority, n + 1, x) for x in exp.split('+')])
    else:
        result = '-'.join([calc(priority, n + 1, x) for x in exp.split('-')])

    return str(eval(result))


def solution(expression):
    answer = 0
    orders = ['*', '+', '-']

    for priority in permutations(orders, 3):
        answer = max(answer, abs(int(calc(priority, 0, expression))))

    return answer
```
문제 풀이에 정답은 없지만 1번 풀이보다는 2번 풀이가 확장성 있고 의도에 맞는 풀이 방식인 것 같다.



