# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (11)(2021.2.2)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 씨름 선수(그리디)

## 문제 해설

* 키 순으로 정렬하기
  * 제일 위의 사람은 키로 모든 사람을 이기는 것
  * 그 아래의 사람은 자신보다 키가 큰 사람보다 몸무게가 많아야 한다.
  * 위를 반복하여 답을 구할 수 있다.
* 최댓값을 갱신하며 진행

## 문제 풀이

```python
n = int(input());
p = []; 
for i in range(n): # 선수 튜플로 입력 받기
    h, w = map(int, input().split());
    p.append((h, w));


ans = 0; # 답
for i in range(n):
    cnt = 0; # 카운트
    for j in range(n):
        if p[i][0] > p[j][0] or p[i][1] > p[j][1]: # 키 또는 몸무게가 클 경우 카운트
            cnt += 1;
    if cnt == n - 1: # 카운트가 n-1이면 답에 1 더하기
        ans += 1;

print(ans);
```



## 문제 답안

```python
n = int(input());
body = [];
for i in range(n):
    a, b = map(int, input().split());
    body.append((a, b));
body.sort(reverse=True) # 키를 기준, 내림차순으로 정렬
largest = 0; # 몸무게의 최대값
cnt = 0;
for x, y in body:
    if y > largest: # 몸무게가 최대값을 갱신할 경우
        largest = y;
        cnt += 1;
print(cnt);
```



## 풀이와 답안 비교

내 코드는 한 사람을 기준으로, 모든 사람과 비교하여 키 또는 몸무게가 큰 경우가 n-1번 반복된다면 답에 체크를 하였다. 하지만, 이중 반복문이 사용되어 많이 비효율적인 코드이다. 

답안의 코드와 같이 한 데이터를 기준으로 내림차순으로 정렬 후 하나의 반복문에 다른 데이터의 최댓값을 갱신하는 방법으로 해결하는 것이 더 효율적이다.



# 2. 창고 정리

## 문제 해설



## 문제 풀이

```python
l = int(input());
st = list(map(int, input().split()));
m = int(input());

for i in range(m):
    st.sort(); # 매번 오름차순 정렬
    st[0] += 1;
    st[l-1] -= 1;
st.sort(); # 재 정렬
print(st[l-1] - st[0]);
```



## 문제 답안

```python
L = int(input());
a = list(map(int, input().split()));
m = int(input());

a.sort()
for _ in range(m):
    a[0] += 1;
    a[L-1] -= 1;
    a.sort();
print(a[L -1]-a[0]);
```



## 풀이와 답안 비교

문제가 이렇게만 나와주면 바랄 것도 없겠다...



# 3. 침몰하는 타이타닉(그리디)

## 문제 해설

* 오름차순 정렬하기
  * 가장 무거운 몸무게의 사람과 가장 가벼운 몸무게의 사람의 조합의 무게를 보기
  * 보트 허용 무게를 초과하는 경우 무거운 사람은 혼자 보트를 탄다.
* **한 명이 남은 경우 고려하기**
* **deque 자료구조를 사용하는 것이 더 효율적**
  * 리스트의 pop은 맨 앞에서 실행할 경우, 삭제 후 다시 당겨오는 작업을 하므로 비효율적이다.
  * 두 개의 포인터를 사용하여, 양쪽에서 삭제와 삽입을 할 수 있다.
  * 큐 + 스택

## 문제 풀이

```python
n, m = map(int, input().split());
a = list(map(int, input().split()));
a.sort() # 오름차순 정렬
cnt = 0; # 구명보트 개수 카운트

while True:
    l = len(a);
    j =0;
    while True:
        boat = 0; # 구명보트 무게
        boat = a[0] + a[l - 1 - j];
        if boat <= m:
            a.pop(0);
            if len(a) == 0: # 리스트가 다 비었을 경우 카운트 하고 끝내기
                cnt += 1;
                break;
            a.pop();
            cnt += 1;
            j +=1;
            break;
        else:
            a.pop(); # 무게 초과시, 끝만 pop
            cnt += 1;
            j += 1;
            break;
    if len(a) == 0: # 리스트가 비면 끝내기
        break;
print(cnt)
    
```



## 문제 답안 1

```python
n, limit = map(int, input().split());
p = list(map(int, input().split()));
p.sort(); # 오름차순 정렬
cnt = 0; # 구명보트
while p: # p가 비어있지 않으면 참
    if len(p) ==1: # 한 명 남은 경우 탈출
        cnt += 1;
        break;
    if p[0] + p[-1] > limit: # 현재 가장 가벼운 사람과 무거운 사람이 제한무게를 넘으면
        p.pop(); # 가장 무거운 한 사람만 탈출
        cnt += 1;
    else:
        p.pop(0); # 가장 가벼운 사람과 무거운 사람 같이 탈출
        p.pop();
        cnt += 1;
print(cnt);
```



## 문제 답안 2

```python
from collections import deque
n, limit = map(int, input().split());
p = list(map(int, input().split()));
p.sort(); # 오름차순 정렬
p = deque(p); # deque 자료구조로 변환
cnt = 0; # 구명보트
while p: # p가 비어있지 않으면 참
    if len(p) ==1: # 한 명 남은 경우 탈출
        cnt += 1;
        break;
    if p[0] + p[-1] > limit: # 현재 가장 가벼운 사람과 무거운 사람이 제한무게를 넘으면
        p.pop(); # 가장 무거운 한 사람만 탈출
        cnt += 1;
    else:
        p.popleft(); # 가장 가벼운 사람과 무거운 사람 같이 탈출
        p.pop();
        cnt += 1;
print(cnt);
```

* **from collections import deque** : deque 자료구조 가져오기
* **.popleft()**: deque 자료구조에서 가장 왼쪽 데이터 pop

## 풀이와 답안 비교

인덱스가 음수이면 뒤에서 셀 수 있다는 것을 응용하자. 그리고 이중 반복문을 쓸 이유도 없었다. 변수의 남발도 자제하자.

 이런 문제에서 **deque 자료구조**가 더 효율적인 것을 잊지말자.



# 4. 증가 수열 만들기(그리디)

## 문제 해설

* 투 포인터 사용하기(이분검색처럼)
* 증가하는 수열을 만들기 위해 빼낸 값을 별도 변수에 저장하기
* 튜플 사용하기

## 문제 풀이

```python
from collections import deque # deque 자료구조 사용하기
n = int(input());
arr = list(map(int, input().split()));
arr = deque(arr); # deque로 변환
upArr = [0] # 증가수열
st = "" # 문자열

while arr: # arr가 빌때 까지 반복
    if arr[0] < arr[-1]: # 왼쪽이 큰 경우
        if arr[0] > upArr[-1]:
            upArr.append(arr.popleft());
            st += "L";
        elif arr[-1] > upArr[-1]:
            upArr.append(arr.pop()); 
            st += "R";
    elif arr[0] > arr[-1]:# 오른쪽이 큰 경우
        if arr[-1] > upArr[-1]: 
            upArr.append(arr.pop()); 
            st += "R";
        elif arr[0]> upArr[-1]:
            upArr.append(arr.popleft());
            st += "L";
    if  arr[0] < upArr[-1] and arr[-1] < upArr[-1]:
        break;

print(len(upArr)-1);
print(st);
```



## 문제 답안

```python
n = int(input());
a = list(map(int, input().split()));
lt = 0; # 시작점
rt = n - 1; # 끝점
last = 0; # 빼낸 값을 저장하는 변수
res="" # 문자열
tmp=[] # 빈 리스트
while lt <= rt:
    if a[lt] > last:
        tmp.append((a[lt], 'L'));
    if a[rt] > last:
        tmp.append((a[rt], 'R'));
    tmp.sort() # 오름차순 정렬
    if len(tmp) == 0: # 수열을 더는 만들 수 없을 때
        break;
    else:
        res = res + tmp[0][1] # 문자열 넣기
        last = tmp[0][0] # 넣은 숫자 저장
        if tmp[0][1] == 'L' : # 왼쪽에서 가져온 경우
            lt += 1;
        else:
            rt -= 1;
    tmp.clear(); # tmp 비우기
print(len(res));
print(res);
```



## 풀이와 답안 비교

내 코드는 별도의 새로운 배열을 생성한다는 점에서 비효율적이다.



# 5. 역수열(그리디)

## 문제 해설

* 역수열의 정의 잘 이해하기
  * 인덱스 번호를 수열의 숫자로 이해하기

|  1   |  2   |  3   |  4   |  5   |  6   |  7   |  8   |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
|  5   |  3   |  4   |  0   |  2   |  1   |  1   |  0   |

* 숫자 1 앞에 0이 5개
* 숫자 2 앞에 0이 3개
* 위와같은 방식으로 찾아내간다.



## 문제 답안

```python
n = int(input());
a = list(map(int, input().split()));
seq = [0] * n;
for i in range(n):
    for j in range(n):
        if a[i] == 0 and seq[j] == 0: # 0을 다 찾고 자리가 비어있을 때;
            seq[j] = i + 1;
            break;
        elif seq[j] == 0:
            a[i] -= 1;
for x in seq:
    print(x, end=' ');
```



## 풀이와 답안 비교

혼자 풀면서, 막히는 것이 많아서 결국 강의를 참고했다. 조건문을 만족하지 않을 때도 반복문이 돈다는 것을 명심하고 풀어야할 것 같다. 이 사실을 자꾸 간과해서 코드 너무 길게 작성하였기 때문에 문제점을 찾기 어려워 풀지 못했다.