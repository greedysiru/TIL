# [프로그래머스] 수식 최대화 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 수식 최대화
from itertools import permutations

import re

# 사용할 수 있는 연산자 리스트를 생성하는 함수
def make_operation_permutations(expression):
    # 주어진 수식에 포함되는 연산자를 넣을 리스트
    operation_list = []
    # 수식에 있는 연산자 넣기
    if '*' in expression:
        operation_list.append('*')
    if '+' in expression:
        operation_list.append('+')
    if '-' in expression:
        operation_list.append('-')

    operation_permutaions = list(permutations(operation_list))

    return operation_permutaions

def solution(expression):
    answer = 0
    # 연산자 순열
    operation_permutations = make_operation_permutations(expression)
    # 정규표현식을 사용하여 수식을 숫자와 연산자로 분리하기
    # [^0 - 9]: 0 ~ 9를 제외한 문자 하나를 찾음
    expression = re.split('([^0-9])', expression)
    # 연산자 순열에서 하나의 값을 뽑고 그 순서대로 계산을 진행하기
    for operation_permutation in operation_permutations:
        # expression을 복사
        copied_expression = expression[:]
        # 연산자 순열의 순서대로 연산자를 뽑아내기
        for operator in operation_permutation:
            # 복사한 수식에서 연산자가 있는 경우
            while operator in copied_expression:
                # 연산자가 존재하는 index
                op_idx = copied_expression.index(operator)
                # *, +, - 를 기준으로 -1, +1 인덱스에 있는 숫자를 연산자로 계산
                if copied_expression[op_idx] == '*':
                    cal = int(copied_expression[op_idx - 1]) * \
                        int(copied_expression[op_idx + 1])
                elif copied_expression[op_idx] == '+':
                    cal = int(copied_expression[op_idx - 1]) + \
                        int(copied_expression[op_idx + 1])
                elif copied_expression[op_idx] == '-':
                    cal = int(copied_expression[op_idx - 1]) - \
                        int(copied_expression[op_idx + 1])
                # 연산자의 이전 index에 값을 넣기
                copied_expression[op_idx - 1] = cal
                # '0번 인덱스 ~ 계산된 값 + 연산자 +2 인덱스 ~ 끝' 슬라이싱으로 복사하기
                copied_expression = copied_expression[:op_idx] + \
                    copied_expression[op_idx + 2:]
        # 수식의 연산자들을 연산자 순열의 순서대로 계산하면 0번 index에 계산 결과가 있음
        # 해당값과 answer의 값을 비교하여 최대가 되는 값으로 answer를 최신화
        answer = max(answer, abs((int(copied_expression[0]))))
    return answer
```



## Comment

항해99에서 제공된 풀이를 보아서 풀었다.

문제를 풀기 위한 핵심 아이디어는 아래 두 가지다.

1. 순열: 수식에서 사용되는 연산자를 리스트화하고 그것을 토대로 순열을 만든다. (**itertools 모듈의 permutations**)
2. 정규표현식: 주어진 수식을 분리하여 연산할 수 있게 한다. (**re 모듈**)

위 두 과정을 거친뒤에는 만들어진 연산자 순열을 하나씩 접근하며 그 순서대로 연산을 진행한다. 연산을 진행하기 전에는 계산된 값을 넣기 위해 기존의 expression을 복사한 변수를 만든다. 연산이 끝나서 새로운 값이 입력되고 나서는 필요한 부분만 슬라이싱으로 복사하여 다시 해당 변수에 할당시킨다. 그 결과로, 순열에 의해 연산이 끝나면 그 변수의 0번 index에는 연산 결과가 있을 것이고 max를 통해서 answer를 매번 순열의 연산이 끝났을 때마다 최신화한다.



# Reference

[프로그래머스](https://programmers.co.kr)

