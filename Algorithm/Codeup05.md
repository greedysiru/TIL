# Codeup: 기초 100제 (41~50) (2020.12.19) 

**사용 언어는 Python입니다.**

## 1. 1043

정수 2개(a,b)를 입력받아 a를 b로 나눈 나머지 출력

```python
a,b = input().split();
a=int(a);
b=int(b);
print(a%b);
```

`%` : Modulus 연산



## 2. 1044

정수 1개 입력받아 1만큼 더해 출력

```python
x = int(input());
print(x+1);
```



## 3. 1045

정수 2개(a,b)를 입력받아 합, 차, 곱, 몫, 나머지, 나눈 값을 출력(소수점 둘째 자리까지)

```python
a,b = input().split();
a = int(a);
b = int(b);
print(a+b);
print(a-b);
print(a*b);
print(a//b);
print(a%b);
x = round(a/b,2);
print("%.2f" %x);
```

`round(a,b)` : a를 소수점 b+1번째 자리에서 반올림



## 4. 1046

정수 3개 입력받아 합과 평균 출력(소수점 첫째 자리까지)

```python
a,b,c = input().split();
a = int(a);
b = int(b);
c = int(c);
print(a+b+c);
print("%.1f" %((a+b+c)/3));
```



## 5. 1047

정수 1개 입력받아 2배 곱해 출력(비트 시프트 연산)

```python
x = int(input());
print(x << 1);
```



### - 비트 시프트 연산

2진수 형태의 값을 지정한 비트 수만큼 밀어주면 2배씩 늘거나 반으로 줄어든다.

`<<` : n만큼 오른쪽에 0이 추가

`>>` : m만큼 왼쪽에 0(양의 정수)이나 1(음의 정수)이 추가



## 6. 1048

정수 2개(a,b)를 입력받아 a를 2<sup>b</sup> 배 곱한 값으로 출력

```python
a,b = input().split();
a=int(a);
b=int(b);
print(a << b);
```



## 7. 1049

정수 2개(a,b)를 입력받아 비교하기1

a > b 면 1, 그렇지 않으면 0

```python
a,b = input().split();
a = int(a);
b = int(b);
if a > b:
  print(1)
else:
  print(0)
```



## 8. 1050

정수 2개(a,b)를 입력받아 비교하기2

a == b 면 1, 그렇지 않으면 0

```python
a,b = input().split();
a = int(a);
b = int(b);
if a == b:
  print(1)
else:
  print(0)
```



## 9. 1051

정수 2개(a,b)를 입력받아 비교하기3

b >= a 면 1, 그렇지 않으면 0

```python
a,b = input().split();
a = int(a);
b = int(b);
if b >= a:
  print(1)
else:
  print(0)
```



## 10. 1052

정수 2개(a,b)를 입력받아 비교하기4

a != b 면 1, 그렇지 않으면 0

```python
a,b = input().split();
a = int(a);
b = int(b);
if a != b:
  print(1)
else:
  print(0)
```

# Reference

https://codeup.kr/problemsetsol.php