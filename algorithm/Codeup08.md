# Codeup: 기초 100제 (71~80) (2020.12.22) 

**사용 언어는 Python입니다.**

## 1. 1073

정수를 순서대로 입력, 0이 아니면 입력된 정수를 출력하고 0이 입력되면 중단 2

```python
X = input().split();
i = 0;
x = int(X[i]);
while x != 0:
  print(x);
  i = i + 1;
  x = int(X[i]);
```



## 2. 1074

정수(1 ~ 100) 1개가 입력되었을 때 카운트다운 출력

```python
x = int(input());
i = 0;
while (i != x):
  print(x-i);
  i = i +1;
```



## 3. 1075

정수(1 ~ 100) 1개가 입력되었을 때 카운트다운 출력 2

처음에 입력한 수 -1 부터 출력

```python
x = int(input());
i = 1;
while (i != x+1):
  print(x-i);
  i = i +1;
```



## 4. 1076

영문자(a ~ z) 1개가 입력되었을 때 그 문자까지의 알파벳 순서대로 출력

```python
A = ord(input());
i = 97;
while( i != A+1):
  print (chr(i));
  i = i +1;
```



## 5. 1077

정수(0 ~ 100) 1개를 입력받아 0부터 그 수까지 순서대로 출력

```python
x = int(input());
for i in range(x+1):
  print(i);
```



## 6. 1078

정수(1 ~ 100) 1개를 입력받아 1부터 그 수까지 짝수의 합 출력

```python
x = int(input());
y = 0;
for i in range(x+1):
  if i % 2 == 0:
    y = y + i;
print(y);
```



## 7. 1079

'q'가 입력될 때까지 입력한 문자를 계속 출력하는 프로그램 작성

```python
A = input().split();
for x in A:
  print(x);
  if ord(x) == ord("q"):
    break;
```



## 8. 1080

1부터 n까지 정수를 계속 더할 때, n보다 같거나 작을 때까지 계속 더하는 프로그램 작성

```python
n = int(input());
y = 0;
for x in range(n):
  y = y + x;
  if y >= n:
    print(x)
    break;
```



## 9. 1081

1부터 n까지, 1부터 m까지 숫자가 적힌 서로 다른 주사위 2개를 던졌을 때 나올 수 있는 모든 경우를 출력

```python
A,B = input().split();
A = int(A);
B = int(B);
for a in range(1,A+1):
  for b in range(1,B+1):
    print(a,b);
```



## 10. 1082

16진수 끼리의 곱하기 출력(A ~ F 입력)

```python
A = int(input(), 16);
for i in range(1,16):
  print(("%X" % A) + "*" + ("%X" % i) + "=" + ("%X" %(A*i)));
```



# Reference

https://codeup.kr/problemsetsol.php