# Codeup: 기초 100제 (61~70) (2020.12.21) 

**사용 언어는 Python입니다.**

## 1. 1063

입력된 두 정수 a,b 중 큰 값을 출력(조건문 사용하지 않고 3항 연산자 사용)

```python
a,b =input().split();
a = int(a);
b = int(b);
print (a if a>b else b);
```

Python의 3항 연산자는 if와 else로 표현



## 2. 1064

입력된 세 정수 a,b,c 중 가장 작은 값을 출력하는 프로그램을 작성(3항 연산자 사용)

```python
a,b,c = input().split();
a = int(a);
b = int(b);
c = int(c);
min = (a if a<b else b);
print(min if min<c else c);
```



## 3. 1065

입력된 세 정수 a,b,c 중 짝수만 출력

```python
a,b,c = input().split();
a = int(a);
b = int(b);
c = int(c);
X = [a,b,c];
for y in X :
  if y % 2 == 0 :
    print(y);   

```

입력된 세 정수 a,b,c를 X에 리스트 저장하고 for문의 변수 y에 2를 모듈러 연산하였을 때 0 이면 짝수이므로 출력



## 4. 1066

입력된 세 정수 a,b,c 의 짝(even)/홀(odd)을 출력

```python
a,b,c = input().split();
a = int(a);
b = int(b);
c = int(c);
X = [a,b,c];
for y in X :
  if y % 2 == 0 :
    print("even");
  else:
  	print("odd");
```



## 5. 1067

입력된 정수 1개를 음(minus)/양(plus)/짝(even)/홀(odd) 출력

```python
a = int(input());
if a < 0:
  if a % 2 == 0:
    print("minus");
    print("even");
  else:
    print("minus");
    print("odd");
else:
  if a % 2 == 0:
    print("plus");
    print("even");
  else:
    print("plus");
    print("odd");
```



## 6. 1068

점수(정수, 0~100)를 입력받아 평가 출력

| 점수 범위 | 평가 |
| :-------: | :--: |
| 90 ~ 100  |  A   |
|  70 ~ 89  |  B   |
|  40 ~ 69  |  C   |
|  0 ~ 39   |  D   |



```python
score = int(input());
if score > 39:
  if score >69:
    if score>89:
      print("A");
    else:
      print("B");
  else:
    print("C");
else:
  print("D");
```



## 7. 1069

평가를 문자로 받아 내용을 다르게 출력

A : best!!!
B : good!!
C : run!
D : slowly~
나머지 문자들 : what?

```python
eval = input();
if eval == "A":
  print("best!!!");
elif eval == "B":
  print("good!!");
elif eval == "C":
  print("run!");
elif eval == "D":
	print("slowly~")
else :
  print("what?")
```



## 8. 1070

월이 입력될 때 계절 이름이 출력

12, 1, 2 : winter
 3, 4, 5 : spring
 6, 7, 8 : summer
 9, 10, 11 : fall

```python
mon = int(input());
if mon>2 and mon!=12:
  if mon>5 and mon!=12:
    if mon>8 and mon<12:
      print("fall");
    else:
      print("summer");
  else:
      print("spring");
else:
  print("winter");
      
```



## 9. 1071

정수를 순서대로 입력, 0이 아니면 입력된 정수를 출력하고 0이 입력되면 중단

```python
X = input().split();
for i in X:
  if int(i) == 0:
    break;
  else:
    print(i); 
```

`breaek` : 해당 조건에서 반복문 중단



## 10. 1072

n개의 정수가 순서대로 입력받아 순서대로 출력

```python
x = int(input());
y = input().split();
for i in y:
  print(i);
```



# Reference

https://codeup.kr/problemsetsol.php