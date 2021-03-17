# [동빈나]이코테 2021 강의 몰아보기(3)(2020.12.31)



**본 내용은 해당 [강의](https://www.youtube.com/watch?v=m-9pAwq1o3w&list=PLRx0vPvlEmdAghTr5mXQxGpHjWqSz0dgC&index=1) 토대로 작성**



# 파이썬 문법 부수기

## 1. 기본 입출력

* 모든 프로그램은 적절한 입출력 양식을 가지고 있다.
* 프로그램 동작의 첫 단계는 데이터를 입력 받거나 생성하는 것



### 자주 사용되는 표준 입력 방법

* **input()** : 한 줄의 문자열을 입력 받는 함수
* **map()** : 리스트의 모든 원소에 각각 특정 함수를 적용할 때 사용하는 함수

```python
# 데이터의 개수 입력
n = int(input())

# 각 데이터를 공백을 기준으로 구분하여 입력
data = list(map(int, input().split())) # 65 90 75 34 99 입력

data.sort(reverse=true) # 내림차순 정렬
print(data)             # [99, 90, 75, 65, 34]

# n, m, k를 공백을 기준으로 구분하여 입력
n, m, k = map(int, input().split()) # 3 5 7 입력

print(n, m, k)                      # 3 5 7 출력
```



### 빠르게 입력 받기

* sys 라이브러리에 정의되어 있는 **sys.stdin.readline()** 메서드 이용
  * 입력 후 엔터(Enter)가 줄 바꿈 기호로 입력되므로 **rstrip()** 메서드를 함께 사용

```python
import sys # sys 라이브러리 불러오기

# 문자열 입력받기
data = sys.stdin.readline().rstrip()
print(data)
```



### 자주 사용되는 표준 출력 방법

* **print()** : Python의 기본 출력
  * 각 변수를 콤마(,)를 이용하여 띄어쓰기로 구분 출력
* 기본적으로 출력 이후에 **줄 바꿈 수행**
  * 원치 않는 경우 **'end'** 속성 이용

```python
# 출력할 변수들
a = 1
b = 2
print(a,b) # 1 2 출력
print(7, end=" ")  # 7 8 나란히 출력
print(8, end=" ")

# 출력할 변수
answer = 7
print("정답은" + str(answer) + "입니다") # 정답은 7입니다. # 정수형 데이터를 문자열로 바꿔 출력해야한다.
```



### f-string 예제

* 파이썬 3.6부터 사용 가능, 문자열 앞에 접두사 **'f'** 를 붙여 사용
* 중괄호 안에 변수명 기입, 간단히 **문자열과 정수를 함께** 넣을 수 있음



## 2. 조건문

* **프로그램의 흐름을 제어**하는 문법
* 조건에 따라 프로그램의 로직을 설정



### 조건문 예제

```python
x = 15
if x >= 10:
    print("x >= 10")

if x >= 0:
    print("x >= 0")
  
if x >= 30:                # x >= 10
    print("x >= 30")         # x >= 0
```



### 들여쓰기

* Python에서는 코드의 블록(Block)을 들여쓰기(Indent)로 지정
  * 블록(Block) : 특정 기능을 수행하기 위한 한 단위의 코드 묶음
  * 조건문 아래에 실행할 것들을 들여쓰기로 묶음

* 탭을 사용하거나 공백 문자(space)를 여러번 사용
  * 표준 : **4개의 공백 문자**

```python
score = 85

if score >= 70:
    print('성적인 70점 이상입니다.')
    if score >= 90:
        print('우수한 성적입니다.')
else:
    print('성적이 70점 미만입니다.')
    print('조금 더 분발하세요.')
    
print('프로그램을 종료합니다.')
```



### 조건문의 기본 형태

* 조건문의 기본 형태는 **if ~ elif ~ else**
  * elif, else는 경우에 따라 사용하지 않아도 된다.

```python
if 조건문 1:
    조건문 1이 True일 때 실행
elif 조건문 2:
    조건문 1에 해당하지 않고, 조건문 2가 True일 때 실행되는 코드
else:
    위의 모든 조건문이 False일 때 실행
```



### 성적 구간에 따른 학점 출력 예제

```python
score = 85

if score >= 90:
    print("학점: A")
elif score >= 80:
    print("학점: B")
elif score >= 70:
    print("학점: C")
else:
    print("학점: F")     # 학점: B 출력
```



### 비교 연산자

* **특정한 두 값을 비교할 때 이용**
  * **대입 연산자(=)**와 **같은 연산자(==)** 유의

| 비교 연산자 |             설명              |
| :---------: | :---------------------------: |
|   X == Y    |   X와 Y가 서로 같을 때 True   |
|   X != Y    |   X와 Y가 서로 다를 때 True   |
|    X > Y    |     X가 Y보다 클 때 True      |
|    X < Y    |    X가 Y보다 작을 때 True     |
|   x >= Y    | X가 Y보다 크거나 같을 때 True |
|   X <= Y    | X가 Y보다 작거나 같을 때 True |



### 논리 연산자

* **논리 값(True / False)**사이의 연산을 수행

| 논리 연산자 |               설명               |
| :---------: | :------------------------------: |
|   X and Y   |   X와 Y가 모두 True일 때 True    |
|   X or Y    | X와 Y중에 하나만 True이어도 True |
|    not X    |       X가 False일 때 True        |



### 기타 연산자

* 다수의 데이터를 담는 자료형을 위해 **in 연산자**와 **not in 연산자** 제공
  * 리스트, 튜플, 문자열, 딕셔너리 모두 사용 가능

| in 연산자와 not in 연산자 | 설명                                     |
| ------------------------- | ---------------------------------------- |
| x in 리스트               | 리스트 안에 x가 들어가 있을 때 True      |
| x not in 문자열           | 문자열 안에 x가 들어가 있지 않을 때 True |



### pass 키워드

* 아무것도 처리하고 싶지 않을 때 **pass 키워드** 사용
  * 디버깅 과정에서 비워놓고 싶은 경우

```python
score = 85

if score >= 80:
    pass # 지나가기
else:
    print('성적이 80점 미만입니다.')
    
print('프로그램을 종료합니다.')         # 프로그램을 종료합니다.
```



### 조건문의 간소화

* 실행될 소스코드가 한 줄인 경우, 줄 바꿈을 하지 않고 간략하게 표현

```python
score = 85

if score >= 80: result = "Success" # Success
else: result = "Fail"
```

* 조건부 표현식(Conditional Expression)은 **if ~ else문을 한 줄에 작성**

``` python
score = 85
result = "Success" if score >= 80 else 'Fail'

print(result) # Success 출력
```



### 조건문 내의 부등식

* 수학의 부등식을 그대로 사용
* **x > 0 and X < 20** 과 **0< x < 20** 는 같다.



## 3. 반복문

* 특정한 소스코드를 **반복적으로 실행**하고자 할 때 사용하는 문법
* Python에서는 while문과 for문을 사용
  * for문이 더 간결함



### 1부터 9까지 모든 정수의 합 구하기 예제 (while문)

```python
i = 1
result = 0

while i <= 9: # 참일 때만 실행
    result += i
    i += 1

print(result) # 45 출력
```



### 1부터 9까지 홀수의 합 구하기 예제 (while문)

```python
i = 1
result = 0

# i가 9보다 작거나 같을 때 아래 코드를 반복적으로 실행
while i <= 9:
    if i % 2 == 1:
      result += i
    i += 1

print(result) # 25 출력
```



### 반복문에서의 무한 루프

* **무한 루프(Infinite Loop)**란 끊임없이 반복되는 반복 구문
  * 코딩 테스트에서 무한 루프를 구현할 일은 거의 없으니 유의
  * 반복문을 작성한 뒤에 항상 반목문을 탈출할 수 있는지 확인

```python
x = 10

while x > 5:
    print(x) # 10 10 10 10 10 10 10 10 ......
```



### 반복문: for문

* 반복문으로 for문을 이용할 수 있다.
* for문의 구조는 아래와 같다. 'in' 뒤에 오는 **데이터(리스트, 튜플 등)에 포함 되어 있는 원소를 첫 번째 인덱스부터 차례대로 하나씩 방문**

>for 변수 in 리스트:
>
>실행할 소스코드

```python
array = [9, 8, 7, 6, 5]

for x in array:
    print(x) # 9 8 7 6 5 하나씩 출력
```

* for문에서 연속적인 값을 차례대로 순회할 때는 **range()**를 주로 사용
  * range(시작 값, 끝 값 + 1) 형태로 사용
  * 기본 시작 값은 0

```python
result = 0

# i는 i부터 9까지의 모든 값을 순회
for i in range(1, 10):
    result += i
    
print(result)  # 45 출력
```



### continue 키워드

* 반복문에서 남은 코드의 실행을 건너뛰고, 다음 반복을 진행하고자 할 때 **continue**를 사용
* 1부터 9까지의 홀수의 합을 구할 때 다음과 같이 작성

```python
result = 0

for i in range(1, 10):
    if i % 2 == 0:
        continue
    result += i
    
print(result)  # 25 출력
```



### break 키워드

* 반복문을 즉시 탈출하고자 할 때 **break**를 사용
* 1부터 5까지 정수를 차례대로 출력하고자 할 때 다음과 같이 작성

```python
i = 1

while True:
    print("현재 i의 값:", i)
    if i == 5:
        break
    i += 1               
```



### 학생들의 합격 여부 판단 예제 1)

점수가 80점만 넘으면 합격

```Python
scores = [90, 85, 77, 65, 97]

for i in range(5):
    if scores[i] >= 80:
        print(i + 1, "번 학생은 합격입니다.") 
```



### 학생들의 합격 여부 판단 예제 2)

특정 번호의 학생은 제외하기

```python
scores = [90, 85, 77, 65, 97]
cheating_student_list = {2, 4}

for i in range(5):
    if i + 1 in cheating_student_list:
        continue                          # 2, 4 제외
    if scores[i] >= 80:
        print(i + 1, "번 학생은 합격입니다.")
```



### 중첩된 반복문: 구구단 예제

```python
for i in range(2, 10):
    for j in range(1, 10):
        print(i, "X", j, "=", i * j)
    print()                             # 2 ~ 9 단 출력
```



## 4. 함수

* 함수(Function)란, 특정한 작업을 하나의 단위로 묶어 놓은 것을 의미
* 함수를 사용하면 불필요한 소스코드의 반복을 줄일 수 있다.



### 함수의 종류

* 내장 함수 : Python이 기본적으로 제공하는 함수
* 사용자 정의 함수 : 개발자가 직접 정의하여 사용할 수 있는 함수



### 함수 정의하기

* 프로그램에는 똑같은 코드가 반복적으로 사용되어야 할 때가 많다.
* 함수를 사용하면 **소스코드의 길이를 줄일 수 있다.**
  * 매개변수 : 함수 내부에서 사용할 변수
  * 반환 값 : 함수에서 처리 된 결과를 반환

>def 함수명(매개변수):
>
>​    실행할 소스코드
>
>​    return 반환 값



### 더하기 함수 예시

```python
# 더하기 함수 예시 1)
def add(a, b):
    return a + b
  
print(add(3, 7))               # 10

# 더하기 함수 예시 2)
def add(a, b):
    print('함수의 결과: ', a + b)
    
add(3, 7)                      # 함수의 결과: 10
```



### 파라미터 지정하기

* **파라미터의 변수를 직접 지정**할 수 있다.
  * 매개변수의 순서가 달라도 상관 없음

```python
def add(a, b):
    print('함수의 결과:', a + b)
    
add(b = 3, a= 7)    # 함수의 결과 10
```



### global 키워드

* **global** 키워드로 변수를 지정하면 해당 함수에서는 지역 변수를 만들지 않고, **함수 바깥에 선언된 변수를 바로 참조

```python
a = 0

def func():
    global a             # 함수 밖 a 참조
    a += 1
    
for i in range(10):
    func()
    
print(a)                 # 10
```



### 지역변수와 전역변수

* 지역변수는 함수 내부에서 선언한 변수
* 전역 변수는 함수 외부에서 선언한 변수
* 단순하게 전역 변수를 참조하는 것은 오류가 나지 않는다.
* 전역 변수로 선언된 개체의 내부 메서드를 호출하기는 가능하다.
* 전역 변수와 지역 변수로 동일한 이름의 변수가 존재한다면, 함수는 지역 변수를 우선적으로 처리.



### 여려 개의 반환 값

* Python에서 함수는 여러 개의 반환 값을 가질 수 있다.

```python
def operator(a, b):
    add_var = a + b
    subtract_var = a - b
    multiply_var = a * b
    divide_var = a / b
    return add_var, subtract_var, multiply_var, divide_var
  
a, b, c, d = operator(7, 3)
print(a, b, c, d)
```



### 람다 표현식

* 람다 표현식을 이용하면 함수를 간단하게 작성
  * 특정한 기능을 수행하는 함수를 한 줄에 작성
  * 함수안에 함수를 사용하는 경우 사용

```python
def add(a, b):
    return a + b

# 일반적인 add() 메서드 사용
print(add(3, 7))                          # 10

# 람다 표현식으로 구현한 add() 메서드
print((lambda a, b: a + b)(3, 7))         # 10
```



### 람다 표현식 예시 : 내장 함수에서 자주 사용되는 람다 함수

```Python
array = [('홍길동', 50), ('이순신', 32), ('이무개', 74)]

def my_key(x):
    return x[1]

  print(sorted(array, key=my_key))
  print(sorted(array, key=lambda x: x[1])) # [('이순신', 32), ('홍길동', 50), ('아무개', 74)]
```



### 람다 표현식 예시: 여러 개의 리스트에 적용

```python
list1 = [1, 2, 3, 4, 5]
list2 = [6, 7, 8, 9, 10]

result = map(lambda a, b: a + b, list1, list2)

print(list(result))              # [7, 9, 11, 13, 15]
```



## 5. 실전에서 유용한 표준 라이브러리

* 내장 함수 : 기본 입출력 함수부터 정렬 함수까지 기본적인 함수들을 ㅈ레공
  * 필수적인 기능을 포함
* itertools : Python에서 반복되는 형태의 데이터를 처리하기 위한 유용한 기능들을 제공
  * 순열, 조합 라이브러리는 코딩 테스트에서 자주 사용
* heaps : 힙(Heap) 자료구조를 제공
  * 일반적으로 우선순위 큐 기능을 구현하기 위해 사용
* bisect : 이진 탐색(Binary Search) 기능을 제공
* collections : 덱(deque), 카운터(Counter) 등의 유용한 자료구조를 포함
* math : 필수적인 수학적 기능 제공
  * 팩토리얼, 제곱근, 최대공약수(GCD), 삼각함수 관련 함수부터 파이(pi)와 같은 상수 포함



### 자주 사용되는 내장 함수

```python
# sum()
result = sum([1, 2, 3, 4, 5])
print(result)                 # 15

# min(), max()
min_result = min(7, 3, 5, 2)
max_result = max(7, 3, 5, 2)
print(min_result, max_result) # 2 7

# eval()
result = eval("(3 + 5) * 7")
print(result)                 #56

# sorted()
result = sorted([9, 1, 8, 5, 4])
reverse_result = sorted([9, 1, 8, 5, 4], reverse=True)
print(result)                 # [1, 4, 5, 8, 9]
print(reverse_result)         # [9, 8, 5, 4, 1]

# sorted() with key
array = [('홍길동', 35), ('이순신', 75), ('아무개', 50)]
result = sorted(array, key = lambda x: x[1], reverse=True)
print(result)                 # [('이순신', 75), ('아무개', 50), ('홍길동', 35)]
```



### 순열과 조합

* 모든 경우의 수를 고려해야 할 때 **itertools** 라이브러리 사용
* 순열 : 서로 다른 n개에서 서로 다른 r개를 선택하여 일렬로 나열
* 조합 : 서로 다른 n개에서 순서에 상관 없이 서로 다른 r개를 선택하는 것



### 순열 라이브러리 사용 예시

```python
from itertools import permutations

data = ['A', 'B', 'C'] # 데이터 준비

result = list(permutations(data, 3)) # 모든 순열 구하기
print(result) # 순열 출력
```



### 조합 라이브러리 사용 예시

```python
from itertools import combinations

data = ['A', 'B', 'C'] # 데이터 준비

result = list(combinations(data, 2)) # 2 개를 뽑는 모든 조합 구하기
print(result) # 조합 출력
```



### 중복 순열과 중복 조합

```python
from itertools import product

data = ['A', 'B', 'C'] # 데이터 준비

result = list(product(data, repeat=2)) # 2개를 뽑는 모든 순열 구하기 (중복 허용)
print(result) # 중복 순열 출력

from itertools import combinations_with_replacement

data = ['A', 'B', 'C'] # 데이터 준비

result = list(combinations_with_replacement(data, 2)) # 2개를 뽑는 모든 조합 구하기 (중복 허용)
print(result) # 중복 조합 출력
```



### Counter

* collections 라이브러리의 **Counter**는 등장 횟수를 세는 기능을 제공
* 리스트와 같은 반복 가능한(iterable) 객체가 주어졌을 때 내부의 원소가 몇 번씩 등장했는지를 알려줍니다.

```python
from collections import Counter

counter = Counter(['red', 'blue', 'red', 'green', 'blue', 'blue'])

print(counter['blue']) # 'blue'가 등장한 횟수 출력
print(counter['green']) # 'green'이 등장한 횟수 출력
print(dict(counter)) # 사전 자료형으로 반환
```



### 최대 공약수와 최소 공배수

* 최대 공약수를 구해야 할 때는 math 라이브러리의 gcd() 함수를 이용할 수 있다.

```python
import math

# 최소 공배수(LCM)을 구하는 함수
def lcm(a, b):
    return a * b // math.gcd(a, b)
  
a = 21
b = 14

print(math.gcd(21, 14)) # 최대 공약수(GCD) 계산
print(lcm(21, 14)) # 최소 공배수(LCM) 계산
```

