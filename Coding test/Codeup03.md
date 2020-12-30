# [Codeup] 기초 100제(21~30) (2020.12.17)

**사용 언어는 Python입니다.**

## 1. 1023

실수 1개를 입력받아 정수부분과 실수 부분으로 나누어 출력하기

```python
a,b = input().split(".");
print(a);
print(b);
```



## 2. 1024

단어 1개 입력받아 나누어 출력하기

```python
x = input();
for i in x:
  print("'%c'" %i)
```

%c는 한글자씩 출력



## 3. 1025

정수 1개 입력받아 나누어 출력하기

```python
n=input();

print("["+str(int(n[0])*10000) +”]”);
print("["+str(int(n[1])*1000) +”]”);
print("["+str(int(n[2])*100) +”]”);
print("["+str(int(n[3])*10) +”]”);
print("["+str(int(n[4])*1) +”]”);
```



## 4. 1026

시, 분, 초 입력받아 분만 출력하기

```python
h,m,s = input().split(“;”);
print(int(m));
```



## 5. 1027

년, 월, 일 입력받아 형식 바꿔 출력하기

```python
y,m,d=input().split(".");
print(d.zfill(2)+"-"+m.zfill(2)+"-"+y.zfill(4));
```



## 6. 1028

정수 1개 입력받아 그대로 출력하기2

```python
x = int(input());
print(x);
```



## 7. 1029

실수 1개 입력받아 그대로 출력하기 2

```python
x = input();
print("%.11f" % float(x));
```

`%.11f` 는 소수점 11자리까지 표시한다는 포맷



## 8. 1030

정수 1개 입력받아 그대로 출력하기 3

6.1028과 동일



## 9. 1031

10진 정수 1개 입력받아 8진수 출력하기

```python
x = int(input());
print(format(x,'o'));
```

format함수로 8진수 변환



## 10. 1032

10진 정수 1개 입력받아 16진수 출력하기

```python
x = int(input());
print(format(x,'x'));
```

# Reference

https://codeup.kr/problemsetsol.php