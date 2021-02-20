# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (6)(2021.1.26 ~ 27)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 자릿수의 합

## 문제 풀이

```Python
n = int(input());                    # 입력 받기
a = list(map(int, input().split())); # 입력 받기

def digit_sum(x): # 자릿수의 합을 구하는 함수 정의
    x = str(x); # 문자열로 변환
    b = [];     # 빈 배열 만들기
    for i in x: # 각 자리의 숫자 뽑아내기
        i = int(i); # 다시 정수로 변환
        b.append(i) # 배열 b에 저장
    return sum(b); # 각 요소의 합을 return

max = 0
maxIndex = 0

for index, value in enumerate(a): # 배열 a의 index와 value를 각각 저장
    if max < digit_sum(value): # 각 자릿수의 합이 최대인 것을 입력하기
        max = digit_sum(value);
        maxIndex = index; # 해당 최댓값의 index 저장

print(a[maxIndex]); # 각 자릿수의 합이 최대인 숫자를 출력
```



## 문제 해설 

* **각 자릿수의 합을 더하는 방법**
  * 해당 수를 10으로 나눈 뒤, 나머지와 몫을 구한다.
  * 몫을 다시 10으로 나눈 뒤, 나머지는 전의 나머지와 더하고 몫은 다시 10으로 나눈다.
  * 몫이 0보다 작거나 같아질 때까지 반복한다.
* **받은 정수를 string 처리하여 해결한다. (다른 방법)**



## 문제 답안 1

```python
n = int(input());                    # 입력 받기
a = list(map(int, input().split())); # 입력 받기

def digit_sum(x):
    sum = 0;
    while x > 0: # x가 0일때 반복문 중단
        sum += x % 10; # x를 10으로 나눈 나머지 더하기
        x = x // 10; # x를 10으로 나눈 몫 x에 대입하기
    return sum

max = -2147000 # 가장 작은 정수 입력
  
for x in a: # a의 자료 하나하나 접근
    tot = digit_sum(x);
    if tot > max: # 최댓값 찾기
        max = tot;
        res = x; # 해당 index 저장
    
print(res);
```



## 문제 답안 2

* 위보다 편리한 방법

```python
n = int(input());                    # 입력 받기
a = list(map(int, input().split())); # 입력 받기

def digit_sum(x):
    sum = 0;
    for i in str(x): # 문자열 변환
        sum += int(i) # 정수로 변환
    return sum

max = -2147000 # 가장 작은 정수 입력
  
for x in a: # a의 자료 하나하나 접근
    tot = digit_sum(x);
    if tot > max: # 최댓값 찾기
        max = tot;
        res = x; # 해당 index 저장
    
print(res);
```







## 풀이와 답안 비교

거의 완벽하게 풀었다고 생각한다. 강사님의 두 번째 방법이랑 거의 비슷하게 풀었다. 다만, 나는 index를 뽑는 과정에서 enumerate를 사용했는데 굳이 쓸 필요가 없다. 반복문에서 index는 반복되는 숫자라고 생각하면 될 것 같다. 

첫 번째 방법은 정수 그대로를 나눗셈과 몫으로 풀어내는 방법이었다. 기억할 필요가 있을 것 같다. 



# 2. 소수의 개수(에라토스테네스 체)

## 문제 풀이

```python
n = int(input());
a = [0 for _ in range(n+1)]; # 배열만들기
cnt = 0;  #소수 세기

for i in range(2, n+1): # 2부터 소수 찾기
    if a[i] == 0:
        cnt += 1; # 소수이므로 +1
        j = 1
        while i * j <= n:
            a[i * j] = 1; # 소수의 배수 check
            j += 1;

print(cnt); # 소수 개수 출력하기        
```



## 문제 해설

* 해당 자연수만큼의 길이를 가지는 배열을 생성한다.(0으로 초기화)
  * 2부터의 ndex 번호 중 소수를 찾는다.
  * index의 번호의 배수는 check한다.
  * check된 index는 소수가 아니다.
  * 소수인 경우 count한다.
  * 배열의 끝까지 반복한다.



## 문제 답안

```python
n = int(input())
ch=[0]*(n + 1); # 리스트 생성
cnt = 0;
for i in range(2, n + 1):
    if ch[i] == 0:
        cnt += 1;
        for j in range(i, n+1, i): # step을 i만큼 준다(배수만큼 증가)
            ch[j] = 1; # 배수인 경우 1 체크
print(cnt);
```



## 풀이와 답안 비교

내 코드는 문제를 잘 풀 수는 있었는데 숫자를 하나하나 탐색하므로 시간이 오래걸리는 코드이다. 강사님의 코드처럼 step을 활용하여 시간을 단축시키는 방법이 더 효율적이다.



# 3. 뒤집은 소수

## 문제 풀이

```python
n = int(input());
arr = list(map(int, input().split())); # 배열로 입력 받기

def reverse(x): # 숫자 뒤집기 함수
    res = 0;
    while x != 0:
        t = x % 10;
        res = res * 10 + t;
        x = x // 10;
    return res;

def inPrime(x): # 소수 판별 함수
    if x == 1: # 1은 무조건 소수가 아니므로
        return False;
    for i in range(2, x): # 2부터 x-1까지 나누어 떨어지면 소수가 아니다.
        if x % i == 0:
            return False
    return True

for i in arr: # 주어진 자연수를 판별
    if inPrime(reverse(i)): # 소수일 때 출력
        print(reverse(i), end=' ');
```



## 문제 해설

* **숫자를 뒤집는 연산**
  1. t = x % 10
  2. res = res * 10 + t
  3. x = x // 10
* **소수 판별은 그 수의 절반까지 하면 된다.**





## 문제 답안

```python
n = int(input());
a = list(map(int, input().split())); # 배열로 입력 받기
def reverse(x): # 뒤집는 함수
    res = 0
    while x>0:
        t = x % 10;
        res = res * 10 + t;
        x = x // 10;
    return res # res 리턴

def isPrime(x): # 소수 판별
    if x == 1: # 1은 소수가 아니므로
        return False
    for i in range(2, x//2): # 절반 판별
        if x % i == 0:
            return False
    else:
        return True
  

for x in a:
    tmp = reverse(x); # 뒤집은 후 tmp에 저장
    if isPrime(tmp):
        print(tmp, end =' ');
```



## 풀이와 답안 비교

역시 내 코드는 비효율 적이었다. 뒤집은 수를 다른 변수에 담았어야 하는데 한번 더 연산을 돌려버렸고 소수 판별식에서 그 수의 절반까지만 판별하면 되는데, 전체를 돌렸으므로 시간은 더 걸릴 것이다. 그리고 숫자를 뒤집는 연산법은 기억해 두는 것이 좋을 것 같다.



# 4. 주사위 게임

## 문제 풀이

```python
maxReward = -2147000;        # 최대 상금
n = int(input()); # 참여하는 사람 수 입력 받기
for i in range(n): # 참여하는 사람 수 만큼 반복하기
    arr = list(map(int, input().split())); # 한 사람 씩 던진 3개의 눈 리스트로 받기
    reward = 0;                  # 상금
    cnt = 0;                     # 같은 눈 세기
    same = 0;                    # 같은 눈 저장
    if arr[0] == arr[1]:         # 눈금이 같은 경우 cnt +1
        cnt += 1;
        same = arr[0];
    if arr[0] == arr[2]:
        cnt += 1;
        same = arr[0];
    if arr[1] == arr[2]:
        cnt += 1;
        same = arr[1];
    if cnt == 0: # 눈금이 하나도 같지 않은 경우
        reward = max(arr) * 100;
    if cnt == 1: # 눈금이 두개가 같은 경우
        reward = 1000 + (same * 100);
    if cnt == 3: # 눈금이 세개가 같은 경우
        reward = 10000 + (same * 1000);
    if maxReward < reward:   # 최대 상금 저장
        maxReward = reward;
print(maxReward)
```



## 문제 해설

* if를 이용해서 조건 별로 처리한다.

## 문제 답안

```python
n = int(input()); # 사람 수 입력 받기
res = 0
for i in range(n): # 사람 수만큼 반복
    tmp = input().split();
    tmp.sort()              # 오름차순 정렬
    a, b, c = map(int, tmp) # 리스트가 정수화 되어서 1:1 로 입력
    if a==b and b==c: # 세 개가 같은 경우
        money = 10000 + a * 1000;
    elif a==b or a==c: # 두 개가 같은 경우(a로 상금 계산)
        money = 1000 + a * 100;
    elif b==c: # 두 개가 같은 경우(b로 상금 계산)
        money = 1000 + b * 100;
    else:
        money = c * 100;
    if money > res:
        res = money;
print(res);
```



## 풀이와 답안 비교

내 코드는 if를 치트키처럼 마구마구 썼다... 그래도 맞추긴했다. 논리 연산자를 써야하고 쓸데없는 조건문을 줄일 필요가 있다. 눈금이 같은 경우를 굳이 분류할 필요가 없었다.



# 5. 점수 계산

## 문제 풀이

```python
n = int(input());                         # 문제의 개수 입력 받기
a = list(map(int, input().split()));    # 문제의 채점 결과 리스트로 받기
score = 0;                                # 점수
cnt = 0;                                  # 연속으로 맞춘 갯수
for i in range(0, len(a)):              # 채점 결과 계산
    if a[i] == 1 and a[i-1] == 1:    # 전 문제를 맞추고 이번 문제도 맞춘 경우
        cnt += 1;                    # 연속으로 맞춘 갯수 +1
        score += cnt;                # 연속으로 맞춘 갯수 만큼 더하기
    elif a[i] == 1:                  # 이번 문제만 맞춘 경우
        score += 1;                  # 점수 +1
        cnt += 1;                    # 연속으로 맞춘 갯수 +1
    elif a[i] == 0:                  # 틀린 경우
        cnt = 0;                     # 연속으로 맞춘 갯수 초기화
print(score);
```



## 문제 답안

```python
n = int(input());
a = list(map(int, input().split()));
sum = 0 # 점수
cnt = 0 # 가중치
for x in a:
    if x == 1:      # 맞을 경우
        cnt += 1;
        sum += cnt;
    else:          # 틀렸을 경우
        cnt = 0;
print(sum);
```



## 풀이와 답안 비교

문제는 잘 풀었으나 코드 작성 시 나는 너무 복잡하게 생각하는 경향이 있다. 간단하게 명료하게 필요한 코드만 작성하도록 하자.