# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (2)(2021.1.23)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 파이썬 기초 문법

 # 1. 반복문(for, while, break, continue)

## range

* 순차적으로 **정수 리스트**를 만든다.

```python
a = range(10); # 순차적으로 0~9까지 정수 리스트를 만든다
print(list(a)); # a를 리스트 자료형으로 출력

----------------------------------------------------------

a = range(1, 10); # 1~9
print(list(a));
```



## for

> for i in rage(시작, 끝, 간격):
>
> ​    반복할 명령어

* **range** 함수와 같이 사용
* 반복할 구문을 들여쓰기한다.

```python
for i in range(10): # 0~9동안 반복(10번)
    print("hello"); # hello 10번 출력
    print(i); # 0~9 각각 출력
    
---------------------------------------------------------

for i in range(10, 0, -1): # 10~0까지 -1하며 반복
    print(i) # 10~0까지 출력
```



## while

> i = 1;
>
> while i의 조건:
>
>    반복할 명령어
>
> ​    i = i + 1;

* while이 조건이 참일 때 명령어 반복 실행
* **무한루프**에 빠지지 않도록 주의

```python
i = 1;
while i <= 10:
    print(i);
    i = i + 1; # 1씩 커지도록 한다.
    
-----------------------------------------------------------------

i = 10;
while i >= 1:
    print(i);
    i = i - 1; # 1씩 작아지도록 한다.
```



## break

* 반복문이 특정 조건일 때 멈추게 할 수 있다.

```python
i = 1;
while True: # 무한 반복
    print(i);
    if i == 10:
        break # i가 10인 경우 break문을 실행하여 반복문 종료
    i += 1 # 축약 연산자
```



## for-else 구문

```python
for i in range(1, 11):
    print(i)
    if i == 5: # 5까지 출력하고 반복문 종료
        break
else:         # for else 구문은 하나이므로 break가 실행되었으므로 아래 명령어는 실행되지 않음
    print(11)
```

* **for-else 구문은 하나**이므로 break가 실행되어 반목문이 종료되면 else또한 실행되지 않는다.
  * for문이 정상적으로 종료된 경우, else를 실행한다.



## continue

* 반복문이 특정 조건일 때 건너 뛰도록 할 수 있다.

```python
for i in range(1, 11):
    if i % 2 == 0: # 짝수인 경우
        continue # continue (건너뛰기)
    print(i); # 1부터 10까지 짝수를 제외하고 출력
```



# 2. 반복문을 이용한 문제 풀이

## 1. 1부터 N까지 홀수 출력하기

```python
n = int(input());
for i in range(1, n + 1):
    if i % 2 == 1:
        print(i);
```



## 2. 1부터 N까지의 합 구하기

```python
n = int(input());
sum = 0;
for i in range(1, n + 1):
    sum += i;
print(sum);
```



## 3. N의 약수 출력하기

```python
n = int(input());
for i in range(1, n + 1):
    if n % i == 0:
        print(i, end=' ');
```



## 3. 중첩 반복문 (이중 for 문)

* for문 안의 for문을 작성할 수 있다.

```python
for i in range(5): # i가 0~4 까지 반복
    print('i: ', i, sep='', end=' ')
    for j in range(5): # j가 0~4 까지 반복
        print('j: ', j, sep='', end=' ');
    print();  # 줄바꿈

'''
i: 0 j: 0 j: 1 j: 2 j: 3 j: 4 
i: 1 j: 0 j: 1 j: 2 j: 3 j: 4 
i: 2 j: 0 j: 1 j: 2 j: 3 j: 4 
i: 3 j: 0 j: 1 j: 2 j: 3 j: 4 
i: 4 j: 0 j: 1 j: 2 j: 3 j: 4
'''
```



### 별 출력하기

```python
for i in range(5):
    for j in range(5):
        print("*", end=' ');
    print();
    
'''
* * * * * 
* * * * * 
* * * * * 
* * * * * 
* * * * * 
'''

-------------------------------------------------------------------------


for i in range(5):
    for j in range(i + 1):
        print("*", end=' ');
    print();
    
'''
* 
* * 
* * * 
* * * * 
* * * * * 
'''

--------------------------------------------------------------------------

for i in range(5):
    for j in range(5 - i):
        print("*", end=' ');
    print();
    
'''
* * * * * 
* * * * 
* * * 
* * 
* 
'''
```



