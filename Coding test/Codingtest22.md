# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (3)(2021.1.23)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 파이썬 기초 문법

# 1. 문자열과 내장함수

## 문자열 내장 함수

```python
msg = "It is Time";

print(msg.upper()); # 대문자화

# IT IS TIME 출력

print(msg.lower());

# it is time

tmp = msg.upper(); # 대문자화된 변수가 입력된다.

print(tmp.find('T')); # T를 찾아 index를 return

print(tmp.count('T')); # T가 몇개 있는지 센다.

print(msg[:2]); # 슬라이스. 처음부터 index 2번 전 까지인 It을 뽑아낸다.

print(msg[3:5]); # 3번부터 4번까지 is 출력

print(len(msg)); # 문자열의 길이를 구한다.
```

* 문자열에서, **공백도 문자 취급**한다
* **.upper()**: 문자열을 대문자화 한다. 결과만 대문자화하고 원래의 문자열은 변하지 않는다.
* **.lower()**: 문자열을 소문자화 한다.
* **.fint()**: 해당하는 문자를 문자열에서 순차적으로 찾아, 처음으로 몇 번째 index에 있는지 return. index는 0번부터 센다.
* **.count()**: 해당하는 문자가 문자열에서 몇 번 나오는 지 카운트한다.
* **슬라이스**
  * **[시작index:마지막index]**: 문자열의 시작 index부터 마지막 index -1 까지 뽑아낸다.
  * **[:마지막 index]**: 문자열의 시작부터 마지막 index-1까지 뽑는다.
* **len()**: 문자열의 길이를 구한다.
  * **for문과 len() 함수를 사용해서** 문자열에 접근할 수 있다.



### for문으로 문자열 접근하기

```python
msg = "It is Time";

for i in range(len(msg)):
    print(msg[i], end=' ');
    
# I t  i s  T i m e 출력

for x in msg: # for문에 문자열을 바로 넣어서 위와 같이 출력할 수 있다.
    print(x, end=' ');
    
-------------------------------------------------------------------------------------

for x in msg:
    if x.isupper(): # x가 대문자이면 참 retrun
        print(x, end=' ');
print()
        
# I T 출력

--------------------------------------------------------------------------------------

for x in msg:
    if x.islower(): # x가 소문자이면 참 return
        print(x, end=' ');
print()

# t i s i m e 출력

--------------------------------------------------------------------------------------

for x in msg:
    if x.isalpha(): # x가 알파벳일 때 참
        print(x, end=' ');
print()

# ItisTime 출력
```

* **.isupper()**: 해당 문자가 대문자이면, true를 return
* **.islower()**: 해당 문자가 소문자이면, true를 retrun
* **.isalpha()**: 해당 문자가 알파벳일 때, true를 return



### ASCII

* 미국 ANSI에서 표준화한 정보교환용 7비트 부호체계
* **A ~ Z == 65 ~ 90**
* **a ~ z == 97 ~ 122**

```python
tmp = 'AZ';

for x in tmp:
    print(ord(x), end=' '); # ASCII number 출력
    
# 65 90 출력

tmp = 'az';

for x in tmp:
    print(ord(x), end=' ');
    
# 97 122 출력

tmp = 65;
print(chr(tmp)) # 숫자를 ASCII 에 대응되는 문자로 출력

# A 출력
```

* **ord()**: 문자를 ASCII number로 변환
* **chr()**: 숫자를 ASCII에따라 대응되는 문자로 출력



# 2. 리스트와 내장함수(1)

* 여러 데이터를 한데 묶을 수 있다.
* **변경할 수 있다.**
* 리스트 생성 방법

> a = []
>
> b = list()
>
> c =[1, 2, 3, 4, 5]

* 호출 방법

> print(a[index 번호])

* index 번호는 0부터 시작한다.

<br>

```python
import random as r # random 모듈을 r로 명령한다.
a = []; # 빈 리스트 생성
b = list(); # 빈 리스트 함수 생성

a = [1, 2, 3, 4, 5]; # 데이터 입력과 동시에 초기화

print(a[0]) # 0번 인덱스 1 출력

b = list(range(1, 11)); # range로 초기화 가능
print(b); # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] 출력

C = a + b;
print(c); # [1, 2, 3, 4, 5, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10] 출력

a.append(6); # 리스트의 제일 뒤에 6 추가
print(a); # [1, 2, 3, 4, 5, 6]

a.insert(3, 7); # a리스트 3번 index에 7을 삽입
print(a); # [1, 2, 3, 7, 4, 5, 6]

a.pop(); # 맨뒤의 데이터 제거
print(a); # [1, 2, 3, 7, 4, 5]

a.pop(3); # 3번 index 제거
print(a); # [1, 2, 3, 4 ,5]

a.remove(4); # 리스트에서 4 제거
print(a); # [1, 2, 3, 5]

print(a.index(5)); # a리스트에서 5라는 값이 있는 index번호 출력

print(sum(b)); # b리스트의 모든 값을 합한 55 출력

print(max(b)); # b리스트에서 제일 큰 값 10 출력

print(min(b)); # b리스트에서 제일 작은 값 1 출력

r.shuffle(b); # a 리스트 무작위로 섞기
print(b);

b.sort(reverse=True) # b리스트 내림차순 정렬
print(b); # [10, 9 ,8 , 7 , 6 , 5, 4, 3, 2, 1]

b.sort() # b리스트 오름차순 정렬
print(b); # [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

b.clear() # b리스트 비우기
```

* **random**: shuffle 내장 함수를 가지고 있는 모듈
* 생성된 리스트 끼리 합연산이 가능하다.
* **.append()**: 리스트의 제일 뒤에 데이터 추가
* **.insert(index 번호, 넣을 데이터)**: 리스트에서 지정한 index번호의 앞(-1)에 데이터를 삽입
* **.pop()**: 맨 뒤의 데이터 제거, index 번호 입력시 해당 index를 삭제한다.
* **.remove()**: 리스트에서 지정한 데이터를 제거한다.
* **.index()**: 리스트에서 지정한 값이 있는  index를 return
* **sum()**: 리스트에 있는 모든 값들을 더한다.
* **max()**: 주어진 인자(리스트)에서 제일 큰 값을 구한다.
* **min()**: 주어진 인자(리스트)에서 제일 작은 값을 구한다.
* **r.shuffle()**: random 모듈의 내장함수 shuffle을 사용하여 리스트를 무작위로 섞는다.
* **.sort()**: 리스트 오름차순 정렬
* **.sort(reverse=True)**: 리스트 내림차순 정렬
* **.clear()**: 빈 리스트로 만들기



# 3. 리스트와 내장함수(2)



```python
a = [23, 12, 36, 53, 19];
print(a[:3]) # 0번 idex부터 3번 index 전까지 슬라이싱[23, 12, 36]
print(a[1:4]) # [12, 36, 53] 출력
print(len(a)) # 리스트의 길이 5 출력

---------------------------------------------------------------------------------------

for i in range(len(a)):
    print(a[i], end=' '); # 리스트 a의 모든 값 접근 23 12 36 53 19 출력
print();

for x in a:
    print(x, end=' '); # 위와 같은 출력
print()

-----------------------------------------------------------------------------------------

for x in a:
    if x % 2 == 1:
        print(x, end=' '); # 홀수 23 53 19 출력
print(); 

-----------------------------------------------------------------------------------------

for x in enumerate(a): # index 번호까지 접근 x는 튜플 자료구조
    print(x);
print();
    
'''

(0, 23)
(1, 12)
(2, 36)
(3, 53)
(4, 19)

'''

for x in enumerate(a):
    print(x[0], x[1]);
print();
    
'''

0 23
1 12
2 36
3 53
4 19

'''

for index, value in enumerate(a):
    print(index, value); # 위와 같은 출력
print()
```

* 문자열처럼 리스트 또한 **슬라이싱**을 할 수 있다.
* **len()**: 리스트에 값이 몇 개 있는지 알려 준다.
* **for문으로 값 하나 하나에 접근**할 수 있다.
* **enumerate()**: 리스트의 index와 value를 **튜플** 로 접근할 수 있다. **(index, value)형식으로 저장.**



## 튜플

* 리스트 처럼 여러 데이터를 저장할 수 있다.
* **변경 불가하다.**
* 튜플 생성 방법

> a = (1, 2, 3, 4, 5)

* 호출 방법

> print(a[index번호])



## all

* 조건에서 리스트의 모든 value가 참이면 참을 return한다.

```python
a = [23, 12, 36, 53, 19];

if all(60>x for x in a): # 모두 참이면 참을 return
    print("YES") # 리스트의 모든 value가 참을 만족하므로 YES출력
else:
    print("NO")
```



## any

* 조건에서 리스트의 value가 하나라도 참이면 참을 return한다.

```python
a = [23, 12, 36, 53, 19];

if any(15>x for x in a): # 한 value가 조건을 만족하면 참 return
    print("YES") # 리스트의 하나의 value가 참을 만족하므로 YES출력
else:
    print("NO")
```



# 4. 2차원 리스트 생성과 접근

* 2차원 리스트는 표로 생각하면 편하다.

```python
a = [[0]*3 for _ in range(3)] # 3개의 1차원리스트(index 0~2) 생성
print(a) # [[0, 0, 0], [0, 0, 0], [0, 0, 0]] 출력
a[0][1] = 1;
a[1][1] = 2;

for x in a:
    print(x);
    
'''
[0, 1, 0]
[0, 2, 0]
[0, 0, 0]
'''

for x in a:
    for y in x:
        print(y, end=' ');
    print()
    
'''
0 1 0 
0 2 0 
0 0 0 
'''
```

| 2차원 리스트 a |       |       | 열번호 |       |
| :------------: | :---: | :---: | :----: | :---: |
|                |       | **0** | **1**  | **2** |
|                | **0** |   0   |   1    |   0   |
|   **행번호**   | **1** |   0   |   2    |   0   |
|                | **2** |   0   |   0    |   0   |



# 5. 함수 만들기

* 함수 정의

> def 함수명(인자1, 인자2):
>
> ​    실행할 명령

*  함수는 **위쪽에 정의**해 놓을 것

```python
def add(a, b):
    c = a + b;
    print(c)
    
add(3, 2); # 5 출력
```



## retrun

* 함수에서 실행 후 **결과를 반환**한다. 
* **함수를 종료**하는 역할

```python
def add(a, b):
  c = a + b;
  return c;

print(add(3, 2)); # 5 출력

x = add(3, 3);
print(x); # 6 출력

---------------------------------------------------------------------------------------------

def add(a, b):
    c = a + b;
    d = a - b;
    return c, d; # c, d 두 개를 return할 수 있다.(튜플)
  
print(add(3, 2)); # (5, 1) 출력
```



### 소수 출력하기

```python
def isPrime(x): # 소수이면 참 return
    for i in range(2, x):
        if x % i == 0:
            return False; # 소수가 아니면 False
    return True;
  
a = [12, 13, 7, 9, 19];

for y in a:
    if isPrime(y): # 함수를 호출하여 소수 판별
        print(y, end=' ') # 13 7 19 출력
```



# 6. 람다 함수

* **익명의 함수** 또는 **표현식**
* **변수**에 할당한다.

>변수명 = lambda 매개변수: 실행할 명령

```python
plus_two = lambda x: x + 2
print(plus_two(1)); # 3 출력
```

* 기본 내장 함수에서 인자로 사용될 때 편리하다.

```python
def plus_one(x):
    return x + 1;

a = [1, 2, 3];
print(list(map(plus_one, a))) # [2, 3, 4] 출력
print(list(map(lambda x: x + 1, a))) # [2, 3, 4] 출력
```

* **map(func, data)**: 받은 자료를 함수 실행