# Codeup: 기초 100제 (51~60) (2020.12.20) 

**사용 언어는 Python입니다.**

## 1. 1053

1(ture, 참) 또는 0(false, 거짓)이 입력되었을 때 반대로 출력

```python
x = bool(int(input()));
x = int(not x);
print(x);
```

`bool` : Boolean

`not` : Boolean을 반대로



## 2. 1054

두 개의 참(1) 또는 거짓(0)이 입력될 때, 모두 참일 때만 참을 출력

```python
a,b = input().split();
a = int(a);
b = int(b);
if a == 1 and b == 1:
  print(1);
else:
  print(0);
```

`and` : 둘 다 참일 때 참을 출력하는 논리연산자



## 3. 1055

두 개의 참(1) 또는 거짓(0)이 입력될 때, 하나라도 참이면 참을 출력

```python
a,b = input().split();
a = int(a);
b = int(b);
if a == 1 or b == 1:
  print(1);
else:
  print(0);
```

`or` : 둘 중 하나가 참이면 참을 출력하는 논리연산자



## 4. 1056

두 개의 참(1) 또는 거짓(0)이 입력될 때, 서로 다를 때 참을 출력

```python
a,b = input().split();
a = int(a);
b = int(b);
if a != b:
  print(1);
else:
  print(0);
```

`XOR` : exclusive or(배타적 논리합), 서로 다를 때 참을 출력하는 논리연산자

`^` : 둘 중 하나만 참일 때 참을 출력하는 비트연산자



## 5. 1057

두 개의 참(1) 또는 거짓(0)이 입력될 때, 참/거짓이 서로 같을 때 참을 출력

```python
a,b = input().split();
a = bool(int(a));
b = bool(int(b));
print(int(not(a^b)));
```



## 6. 1058

두 개의 참(1) 또는 거짓(0)이 입력될 때, 모두 거짓일 때 참을 출력

```python
a,b = input().split();
a = int(a);
b = int(b);
if a==0 and b==0:
  print(1);
else:
  print(0);
```



## 7. 1059

입력 된 정수를 비트단위로 참/거짓을 바꾼 후 정수로 출력

```python
x = int(input());
print(~x);
```

`~n` : tilde, n을 비트단위로 1->0,0->1, 컴퓨터의 음수 표현법



## 8. 1060

입력된 정수 두 개를 비트단위로 and 연산 후 정수로 출력

```python
a,b = input().split();
a = int(a);
b = int(b);
print(a & b);
```

`&` : ampersand, 비트단위로 and 연산



## 9. 1061

입력된 정수 두 개를 비트단위로 or 연산 후 정수로 출력

```python
a,b = input().split();
a = int(a);
b = int(b);
print(a | b);
```

`|` : vertical bar, 비트단위로 or 연산



## 10. 1062

입력된 정수 두 개를 비트단위로 xor 연산 후 정수로 출력

```python
a,b = input().split();
a = int(a);
b = int(b);
print(a ^ b);
```

`^` : xor, circumflex, caret, 비트단위로 xor 연산

# Reference

https://codeup.kr/problemsetsol.php