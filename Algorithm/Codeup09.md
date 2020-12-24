# Codeup: 기초 100제 (81~90) (2020.12.23) 

**사용 언어는 Python입니다.**



## 1. 1083

369 게임을 이기는 프로그램 작성

```python
x = int(input());
for i in range(1,x+1):
  if i % 3 ==0:
    print("X");
  else:
    print(i);
```



## 2. 1084

빨강(r), 초록(g), 파랑(b)을 다르게 섞어 만들 수 있는 모든 경우의 조합과 총 가짓수 계산

```python
r,g,b = input().split();
r = int(r);
g = int(g);
b = int(b);
x = 0
for i in range(r):
  for j in range(g):
    for k in range(b):
      print(i,j,k);
      x = x+1;
print(x);      
```



## 3. 1085

1초 동안 마이크로 소리 걍악을 체크하는 수 : h

한 번 체크한 결과를 저장하는 비트 : b

좌우 등 소리를 저장할 트랙 개수인 채널 : c

녹음할 시간 : s

필요한 저장 용량을 계산하는 프로그램 작성

```python
h,b,c,s = input().split();
h=int(h);
b=int(b);
c=int(c);
s=int(s);
bit = (h*b*c*s);
byte = (bit/8);
kb = (byte/1024);
mb = (kb/1024);
print(str(round(mb,1))+" MB");
```



## 4. 1086

가로 해상도 : w

세로 해상도 : h

한 픽셀을 저장하기 위한 비트 : b

필요한 저장 용량을 계산하는 프로그램 작성

```python
w,h,b = input().split();
w = int(w);
h = int(h);
b = int(b);
print("%.2f MB" % (w*h*b/8/1024/1024));
```



## 5. 1087

1부터 n까지 정수를 계속 더할 때, 언제 입력한 수보다 같거나 커지는지 알아보는 프로그램 작성

```python
x = int(input());
S = 0;
for i in range(x+1):
  S = S + i;
  if S>x or S==x:
    print(S);
    break;
```



## 6. 1088

1부터 입력한 정수까지 1씩 증가시켜 출력하는 프로그램 작성(3의 배수는 제외)

```python
x = int(input());
for i in range(1,x+1):
  if i % 3 == 0:
    i = i+1
  else:
    print(i);
```



## 7. 1089

시작 값(a), 등차(d), 몇 번째인지를 나타내는 정수(n)가 입력될 때, n번째 수 출력

```python
a,d,n = input().split();
a = int(a);
d = int(d);
n = int(n);
x = a;
i = 1;
while (i < n):
  x = x + d;
  i = i + 1;
print(x);
```



## 8. 1090

시작 값(a), 등비(r), 몇 번째 인지를 나타내는 정수(n)가 입력될 때, n번째 수 출력

```python
a,r,n = input().split();
a = int(a);
r = int(r);
n = int(n);
x = a;
i = 1;
while (i < n):
  x = x * r;
  i = i + 1;
print(x);
```



## 9. 1091

시작 값(a), 곱할 값(m), 더할 값(d), 몇 번째 인지를 나타내는 정수(n)가 입력될 때, n번째 수 출력

```python
a,m,d,n =input().split();
a = int(a);
m = int(m);
d = int(d);
n = int(n);
x = a;
i = 1;
while (i<n):
  x = x * m + d;
  i = i + 1;
print(x);
```



## 10. 1092

같은 날 동시에 가입한 인원 3명이 각각의 규칙을 가지고 방문할 때, 다시 함께 방문하게 되는 날을 출력

```python
a,b,c = input().split();
a = int(a);
b = int(b);
c = int(c);
i = 1;
while (i%a!=0 or i%b!=0 or i%c!=0):
  i = i+1;
print(i);
```

최소공배수는 세 수를 각각 나누었을 때, 0이 나온다. 하나의 수라도 나누어 떨어지지 않는다면 반복해야하므로 위의 while문을 쓴다. 

즉, `i%a==0 and i%b==0 and i%c==0` 일때, 반복문을 빠져나가 최소공배수를 출력한다.



# Reference

https://codeup.kr/problemsetsol.php

