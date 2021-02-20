# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (12)(2021.2.3)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 가장 큰 수

## 문제 해설

* 순서를 유지하되, 가장 큰 수가 되도록 숫자를 제거

* **어느 숫자가 있을 때, 그 숫자의 앞에 자신보다 작은 숫자가 없어야 한다.**

  * 위 규칙으로 리스트화를 하면, 내림차순으로 정렬된다.

* **스택 자료 구조 사용하기**

  * **LIFO**(Last In First Out): 후입선출
  * 리스트의 **append, pop**이 스택과 같은 개념

  

## 문제 답안

```python
num, m = map(int, input().split());
num = list(map(int, str(num))); # str로 변환하면 하나하나 접근하여 리스트화
stack = []; # 빈 리스트 만들기
for x in num:
    while stack and m > 0 and stack[-1] < x: # 스택의 마지막 자료가 숫자의 처음보다 작을 떄
        stack.pop();
        m -= 1;
    stack.append(x);
if m != 0:
    stack = stack[:-m];
res = ''.join(map(str. tack)); # join으로 붙여서 출력하기
print(res);
```



## 풀이와 답안 비교

문제의 핵심을 잘 이해하지 못하고 헤매다가 결국 풀지 못하였다. 정확히 문제에서 답을 도출하기 위한 알고리즘을 코드로 똑바로 구현했는지 확인하자.



# 2. 쇠막대기

## 문제 해설

* 스택 자료구조 사용하기
* **여는 괄호 다음에 여는 괄호가 오면, 쇠막대이다.**
* **여는 괄호는 스택에 append**
* **닫는 괄호를 만났을 때 바로앞에 여는 괄호가 있으먼 pop**
* **이때, 스택의 length는 쇠막대의 개수이다.**
* **쇠막대의 닫는 괄호를 찾았을 때는 개수에 1을 더한다.**

## 문제 풀이

```python
a = list(input());
stack = []; # 스택
sticks = 0; # 쇠막대의 수
for i in range(len(a)): # a를 탐색
    if a[i] == '(': # 여는 괄호일 때
        stack.append(a[i]); # 해당 괄호를 스택에 넣기
    elif a[i] == ')': # 닫는 괄호일 때
        if a[i - 1] == ")": # 쇠막대일 때
            stack.pop();
            sticks += 1;
        elif stack[-1] == '(': # 레이저일 때
            stack.pop(); # 레이저 제거
            sticks += len(stack); # 쇠막대의 수는 스택의 길이
print(sticks);
```



## 문제 답안

```python
s = input();
stack = [];
cnt = 0; # 쇠막대기
for i in range(len(s)):
    if s[i] == '(': # 여는 괄호
        stack.append(s[i]);
    else: # 닫는 괄호
        stack.pop(); # 스택의 마지막 pop
        if s[i - 1] == '(': # 레이저인 경우
            cnt += len(stack);
        else: # 쇠막대기의 끝인 경우
            cnt += 1;
print(cnt);
```



## 풀이와 답안 비교

잘 풀었다.