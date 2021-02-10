# [코드잇] 프로그래밍 시작하기 in Python (2021.2.9)



**상세 내용 [블로그](https://greedysiru.tistory.com/180) 참고**



# 파이썬 첫 걸음

## 사용할 도구들

### Python interpreter

* Python -> Python interpreter -> computer
* **Python 코드를 컴퓨터가 이해할 수 있는 기계어(Machine Code)로 번역해주는 프로그램**



### PyCharm

* 코딩을 편하게 해주는 프로그램
* 올인원 솔루션
* **통합 개발 환경(IDE, Intergrated Development Environment)**



# 프로그래밍 기본 개념

## 01. 자료형 개요

### 프로그래밍이란?

* 계산한 수식들을 **컴퓨터에게 알려주는 것**



### 자료형 (Data Type)

* 숫자
  * 정수(Integer)
  * 실수(Floating Point)
* 문자열(String)
  * 따옴표("")로 표현
  * +로 문자열 끼리 합칠 수(붙일 수) 있다.
* 불린(Boolean)
  * 참(True)
  * 거짓(False)



## 02. 추상화 개요

### 추상화(Abstraction)

* 복잡한 것은 숨기고 주요 기능에만 신경 쓰는것
* 변수 (Variable)
* 함수 (Function)
* 객체 (Object)



### 변수 (Variable)

* 값을 저장

```python
x = 254
y = 317
print(x + y);
```



### 함수 (Function)

* 명령을 저장

```python
print("Hello World");
```



## 03. 변수

* 데이터를 어떤 공간에 담아 이름표를 붙여주는 것
* = : **지정 연산자.** 오른쪽의 값을 왼쪽의 변수에 지정
* 복잡한 값을 외울 필요가 없다.
* **그 자체로 코드의 설명**이 되어준다.
  * 변수이름을 잘 짓는 것도 중요하다.
* **코드 수정이 용이**하다.



## 04. 함수

* 내장함수 : print처럼 자주 사용되는 함수. 기본적으로 언어에서 지원한다.
* 어떤 한 기능을 수행하는 긴 명령어들을 함수로 정의해서 호출하면 효율적이다.



### 함수 정의

> def 함수명(파라미터):
>
> ​	실행할 명령

* 함수의 첫 줄: **header**



## 05. 파라미터

> def 함수명(파라미터):
>
> ​	실행할 명령

* 파라미터는 값을 전달받아 함수안의 명령어를 전달받은 값을 이용하여 실행하게 할 수 있다.

```python
def callName(name):
    print(name);
```



## 06. 여러개의 파라미터

> def 함수명(파라미터1, 파라미터2, ...):
>
> ​	실행할 명령

* 함수의 파라미터는 여러개를 가질 수 있다.

```python
def totalSum(num1, num2, num3):
    print(num1 + num2 + num3);
```



## 07. return문

* **함수에서 다른 정보를 돌려주는 것**

```python
def sum(num1, num2, num3):
    return num1 + num2 + num3

x = sum(1, 2, 3);

print(x); # 6 출력
```



# Reference

[코드잇 - 컴퓨터 개론](https://www.codeit.kr/courses/intro-to-computer)