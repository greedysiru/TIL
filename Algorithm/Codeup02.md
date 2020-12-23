# [Codeup] 기초 100제(11~20) (2020.12.16)

**사용 언어는 Python입니다.**

## 1. 1012

실수형으로 변수를 입력하고 그 변수에 실수값을 저장 후 출력

```python
x = float(input());
print("%f" %x);
```

%f: 부동 소수점



## 2. 1013

정수(int) 2개를 구분하여 입력 후 구분하여 출력

```python
a,b = input().splilt();
n = int(a);
m = int(b);
print(a,b);
```

split: 입력값 구분



## 3. 1014

2개의 문자를 구분하여 입력 후 순서를 반대로 출력

```python
a,b = input().split();
print(b,a);
```



## 4. 1015

실수를 입력받고 둘째 자리까지 출력

```python
x = float(input);
print("%.2f" %x);
```



## 5. 1017

정수 1개 입력받아 공백으로 구분하여 세 번 출력

```python
x = int(input());
print(x ,x ,x );
```



## 6. 1018

시간을 입력받고 ":"으로 구분해서 출력

```python
h,m = input().split(":");
print( h + ":" + m );
```



## 7. 1019

연, 월, 일 입력받아 "."로 구분해서 출력

```python
y,m,d = input().split(".");
print(y.zfill(4) + "." + m.zfill(2) + "." + d.zfill(2));
```

`zfill` : 지정한 길이만큼 채워지지 않으면 0으로 빈자리를 채움



## 8. 1020

주민번호 "-" 구분 되어 입력한 후 "-" 생략하여 출력

```python
code1, code2 = input().split("-");
print(code1+code2);
```



## 9. 1021

단어 1개 입력받아 그대로 출력

```python
word = input();
print(word);
```



## 10. 1022

문장 1개 입력받아 그대로 출력

위와 동일

# Reference

https://codeup.kr/problemsetsol.php