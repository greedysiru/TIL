# [항해99 1기] [Chapter2-1] 자료구조, 알고리즘 (1) (2021.3.5)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**

# 10869

[문제 링크](https://www.acmicpc.net/problem/10869)

```python
a, b = map(int, input().split())
print(a + b)
print(a - b)
print(a * b)
print(int(a / b))
print(a % b)
```



## comment

고작 일주일 안 풀었다고 여기서 막히다니... 정수화를 하지 않아 오답처리가 되었었다.



# 2588

[문제 링크](https://www.acmicpc.net/problem/2588)

```python
a = input()
b = input()
for i in range(-1, -4, -1):
    print(int(a) * int(b[i]))
print(int(a) * int(b))
```



# 2884

[문제 링크](https://www.acmicpc.net/problem/2884)

## 오답

```python
# 하루의 시간은 24시간
# 24시간은 24 * 60 = 1440 분
# 자정을 기준으로 700분을 넘기면 11시 40분
# 연산으로 표현하려면 700 // 60 = 11, 700 % 60 = 40
h, m = map(int, input().split())
# 시간을 분으로 변환 후 주어진 분과 합치기
minutes = (60 * h) + m
# 45분 빼기
if minutes > 45:
    minutes -= 45
else:
    minutes = 1440 - (45 - minutes)
# 다시 시간과 분으로 변환
h = minutes // 60
m = minutes % 60

print(h, m, end=" ")
```

이건 왜 틀렸을까?

## 정답

```python
# 하루의 시간은 24시간
# 24시간은 24 * 60 = 1440 분
# 자정을 기준으로 700분을 넘기면 11시 40분
# 연산으로 표현하려면 700 // 60 = 11, 700 % 60 = 40
h, m = map(int, input().split())
# 시간을 분으로 변환 후 주어진 분과 합치기
minutes = (60 * h) + m
# 45분 빼기
minutes -= 45
# 다시 시간과 분으로 변환
h = minutes // 60
m = minutes % 60
# h가 -1인경우 23으로 변환
if h == -1:
    h = 23
print(h, m, end=" ")
```



## comment

첫번째 코드는 30프로 정도 가다가 오답처리 되었다. 왜일까?



# 1110

[문제 링크](https://www.acmicpc.net/problem/1110)

```python
num = int(input())
# 사이클
cycle = 0

n = num

while True:
    a = n // 10
    b = n % 10
    c = a + b
    n = (b * 10) + (c % 10)
    cycle += 1
    if n == num:
        print(cycle)
        break
```



## comment

굿!