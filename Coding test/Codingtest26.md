# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (7)(2021.1.27)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**

# 1. 회문 문자열 검사

## 문제 해설

* 문자열 비교는 그 길이의 반만큼 하면 된다.
* python의 index는 -로 접근할 수 있다.

|   0    |   1    |   2    |   3    |   4    |
| :----: | :----: | :----: | :----: | :----: |
|   L    |   E    |   V    |   E    |   L    |
| **-5** | **-4** | **-3** | **-2** | **-1** |



## 문제 풀이

```python
import sys
sys.stdin = open("in5.txt", "rt")
n = int(input());
for i in range(n):
    str = input(); # 문자열 입력받기
    str = list(str.lower()); # 문자열을 소문자화 후 리스트화
    revStr = [];  # 뒤집은 문자열을 넣을 변수
    for j in range(len(str) - 1, -1, -1): # 뒤집은 문자열 넣기
        revStr.append(str[j]);
    if str == revStr: # 문자열과 뒤집은 문자열 비교
        print("#%d YES" %(i + 1));
    else:
        print("#%d NO" %(i + 1));
```



## 문제 답안 1

```python
n = int(input());
for i in range(n): # n만큼 반복
    s = input(); # 문자열 받기
    s= s.upper(); # 문자열 대문자화
    size = len(s); # 문자열의 길이
    for j in range(size//2): # 길이의 반만 탐색
        if s[j] != s[-1-j]:  # 문자열의 앞뒤가 같지 않을 경우
            print("#%d NO" %(i + 1));
            break          # 문구 출력 후 반복문 중단
    else: 
        print("#%d YES" %(i + 1)); # 이상없이 끝난경우
```



## 문제 답안 2

```python
n = int(input());
for i in range(n): # n만큼 반복
    s = input(); # 문자열 받기
    s= s.upper(); # 문자열 대문자화
    if s == s[::-1]: # 거꾸로 reverse 
        print("#%d YES" %(i + 1));
    else:
        print("#%d No" %(i + 1));
```



## 풀이와 답안 비교

이번에는 비교적 잘 풀었는데, 문자열을 전부 탐색하지말고 답안1처럼 반만 탐색하는 것이 더 효율적일 것이다. 그리고 내 코드는 문자열 전부를 뒤집고 다시 변수에 담고 비교했는데, 답안 1은 뒤집는 과정 없이 index를 이용해서 비교할 수 있었다.

답안 2는 짧고 간단한 코드이긴하나, 강사님 말로는 시험에 사용하는 것은 지양하라고 하셨다.



# 2. 숫자만 추출

## 문제 해설

* 입력 받은 문자열에서 숫자를 판별하기
  * **isdigit()**
  * **isdeciaml()**
* 정수 변환 시 첫자리에서 연속하는 0을 무시하는 연산 사용하기
  * **res = res*10 +int(x)**

## 문제 풀이

```python
str = input();
arrDigit = []; # 숫자를 받는 배열
for i in str:
    if i.isdigit():
        arrDigit.append(i); # 배열에 숫자 넣기

digitLen = len(arrDigit); # 배열 길이 저장
digit = 0; # 숫자
for j in range(digitLen, 0, -1): # 정수화 하기
    digit += int(arrDigit[-j])*(10**(j-1))
print(digit);
cnt = 0; # 약수 세기
for k in range(1, digit + 1):
    if digit % k == 0:
        cnt += 1;
print(cnt);
```



## 문제 답안

```python
s = input();
res = 0;
for x in s:
    if x.indecimal(): # 숫자인 경우
        res = res*10 + int(x); # 첫자리에서 연속하는 0 무시하여 넣기
print(res);
cnt = 0
for i in ragne(1, res + 1): # 약수 카운트
    if res % i == 0:
        cnt += 1;
print(cnt);
```



## 풀이와 답안 비교

res를 잊지말자! 곧바로 수를 받을 수 있다.



# 3. 카드 역배치

## 문제 해설

* 두 변수 스와프
  * a, b = b, a

## 문제 풀이

```python
cards = list(range(21)); # 0부터 20까지 카드 리스트 생성

for _ in range(10): # 10개의 구간 입력 받기
    a, b = map(int, input().split());
    for i in range((b - a + 1)//2): # b-a +1 후 반만큼 바꾸는 작업 하기
        cards[b - i], cards[a + i] = cards[a + i], cards[b - i];

for j in range(1, len(cards)): # 출력하기
    print(cards[j], end=" ")
```



## 문제 답안

```python
a = list(range(21)) # 0~ 20까지 리스트 생성
for _ in range(10): # 10번의 구간 받은 만큼 반복
    s, e = map(int, input().split()); # 입력 받기
    for i in range((e - s + 1)//2): # 카드 바꾸기
        a[s + i], a[e - i] = a[e - i], a[s + i];
a.pop(0) # 0번 인덱스 없애기
for x in a:
    print(x, end =' ');
```



## 풀이와 답안 비교

도중에 혼자 힘으로 풀기 힘들어서 조금은 강의를 참고했지만 만족스럽게 잘 푼 것 같다.



# 4. 두 리스트 합치기

## 문제 해설

* **sort()를 사용하면 시간 복잡도가 높아진다. 사용하지 말 것**
* 문제의 주어진 두개의 정렬은 각각 오름차순 정렬되어있다.
* **포인터 변수를 사용할 것**

|   p1   |   0   |   1   |   2   |       |       |       |       |       |
| :----: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|   a    |   1   |   3   |   5   |       |       |       |       |       |
| **p2** | **0** | **1** | **2** | **3** | **4** |       |       |       |
|   b    |   2   |   3   |   6   |   7   |   9   |       |       |       |
|        | **0** | **1** | **2** | **3** | **4** | **5** | **6** | **7** |
|   c    |   1   |   2   |   3   |   3   |   5   |   6   |   7   |   9   |



## 문제 풀이

```python
import sys
sys.stdin = open("in5.txt", "rt")
n = int(input());
a = list(map(int, input().split()));
m = int(input());
b = list(map(int, input().split()));
c = [] # 합칠 배열을 받을 빈 배열
p1 = 0 # a배열의 포인터 변수
p2 = 0 # b배열의 포인터 변수
for _ in range(n + m): # n + m 번 작업하기
    while p1<n and p2<m:
        if a[p1] < b[p2]:
            c.append(a[p1]);
            p1 += 1;
        else:
            c.append(b[p2]);
            p2 += 1;
if p1 == n:
    for _ in range(n + m - p1):
        c.append(b[p2]);
else:
    for _ in range(n + m - p2):
        c.append(a[p1]);
for i in c:
    print(i, end=' ');
```



## 문제 답안

```python
n = int(input());
a = list(map(int, input().split()));
m = int(input());
b = list(map(int, input().split()));
p1 = p2 = 0; # 투 포인터
c=[];
while p1<n and p2>m:
    if a[p1] <= b[p2]:
        c.append(a[p1]);
        p1 += 1;
    else:
        c.append(b[p2]);
        p2 += 1;
if p1 < n:
    c = c + a[p1:] # p1부터 끝까지
if p2 < m:
    c = c + b[p2:] # p2부터 끝까지
for x in c:
    print(x, end=' ');
```



## 풀이와 답안 비교

내 코드는 3번 문제까지는 잘 풀었으나, 4번, 5번의 긴 문장에서 일부가 출력되지 않았다. 슬라이싱 기능을 이용해서 남은 리스트를 삽입했어햐 했다.



# 5. 수들의 합

## 문제 해설

* 연속적인 수열의 부분 수열의 합 구한 후 특정 수를 만족하는 경우의 수 구하기
  * **부분합 문제**

## 문제 풀이

```python
n, m = map(int, input().split());
arr = list(map(int, input().split()));

e = 0; # 끝 포인터
cnt = 0; # 부분합 카운트
arrSum = 0; # 부분합

for s in range(n): # 시작 포인터를 1 증가시키기
    while e < n and arrSum < m: # 끝 포인터가 끝나기 전에 부분합이 m보다 작은 경우
        arrSum += arr[e];
        e += 1;
    if arrSum == m: # 부분합이 m을 만족하면 카운트하기
        cnt += 1;
    arrSum -= arr[s] # 부분합이 m과 큰거나 같은 경우 s의 위치만큼 빼고 s가 증가
print(cnt);
```



## 문제 답안

```python
n, m = map(int, input().split());
a = list(map(int, input().split()));
lt = 0  # 시작점
rt = 1  # 끝점
tot = a[0] # 부분합
cnt = 0
while True: # 무한반복문
    if tot < m:
        if rt < n:
            tot += a[rt]
            rt += 1;
        else:
            break # 반복문 종료
    elif tot == m:
        cnt += 1;
        tot -= a[lt]
        lt += 1
    else:
        tot -= a[lt];
        lt += 1
print(cnt);
```



## 풀이와 답안 비교

이번만큼은 내 코드가 좀 더 이해가 잘 되고 명료한 것 같다.

