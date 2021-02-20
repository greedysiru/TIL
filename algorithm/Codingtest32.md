# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (13)(2021.2.4)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 후위표기식 만들기

## 문제 해설

* 중위표기식 : 연산 우선 순위에 따라 순차처리를 하지 못함. 컴퓨터가 처리하기 힘들다.

  * 3+5*2/(7-2)

* 후위표기식 : 컴퓨터가 연산 우선 순위에 따라 순차처리 할 수 있다. **스택 자료구조** 

  * 352*72-/+

* 중위표기식에서 후위표기식으로 변환할 때도 **스택 자료구조** 사용

  * 숫자는 바로 출력
  * 연산자는 **우선순위에따라 스택에 저장 or 출력**
  * **여는괄호**는 만났을 때 **스택에 append**
  * **닫는괄호** 만났을 때는 **여는 괄호 전까지의 연산자들 처리**

  

## 문제 답안

```python
a = input();
stack = [];
res = ''; # 출력할 변수
for x in a: # 문자 탐색
    if x.isdecimal(): # 피연산자인 경우
        res += x;
    else:
        if x == '(': # 여는괄호
            stack.append(x);
        elif x == '*' or x == '/': # 곱하기, 나누기인경우
            while stack and (stack[-1] == '*' or stack[-1] == '/'):
                res += stack.pop();
            stack.append(x);
        elif x == '+' or x == '-' : # 덧셈, 뺄셈인 경우
            while stack and stack[-1] != '(': # 여는 괄호가 없으면 연산자 빼기
                res == stack.pop;
            stack.append(x);
        elif x ==')': # 닫는괄호 만났을 떄
            while stack and stack[-1] != '(':
                res += stack.pop()
            stack.pop(); # 여는괄호 없애기
               
while stack: # 연산자 빼기
    res += stack.pop();
print(res);
```



## 풀이와 답안 비교

어렵다. while문에 익숙해져야한다.



# 2. 후위식 연산

## 문제 해설

* 연산자를 만나면 피연산자(숫자)는 앞의 두개의 숫자이다.
* **스택에 먼저 들어간 숫자를 뺄셈과 나누기를 할 때 유의**

## 문제 풀이

```python
postfix = list(input());
stack = [] # 숫자를 저장할 스택
for x in postfix:
    if x.isdecimal(): # 숫자인 경우 스택에 저장
        stack.append(x);
    else:
        if x == "+":
            stack.append(int(stack.pop()) + int(stack.pop()));
        elif x == "-":
            stack.append(int(stack.pop(0)) - int(stack.pop()));
        elif x == "*":
            stack.append(int(stack.pop()) * int(stack.pop()));
        elif x == "/":
            stack.append(int(stack.pop(0)) / int(stack.pop()));
print(stack[0]);
```



## 문제 답안

```python
a = input();
stack = [];
for x in a:
    if x.isdecimal():
        stack.append(int(x)); # 정수화
    else:
        if x == '+':
            n1 = stack.pop();
            n2 = stack.pop();
            stack.append(n2 + n1);
        elif x == '-':
            n1 = stack.pop();
            n2 = stack.pop();
            stack.append(n2 - n1);
        elif x == '*':
            n1 = stack.pop();
            n2 = stack.pop();
            stack.append(n2*n1);
        elif x == '/':
            n1 = stack.pop();
            n2 = stack.pop();
            stack.append(n2/n1);
print(stack[0]);
```



## 풀이와 답안 비교

good

