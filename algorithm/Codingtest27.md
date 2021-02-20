# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (8)(2021.1.28 ~ 29)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 격자판 최대합

## 문제 해설

* 2차원 배열 문제



## 문제 풀이

```python
n = int(input());
arr = [list(map(int, input().split())) for _ in range(n)]; # 2차원 리스트로 입력 받기
arrSum = 0 ; # 합
maxSum = 0; # 최대합

for i in range(n): # 각 행의 합 최대 구하기
    for j in range(n):
        arrSum += arr[i][j];
    if maxSum < arrSum:
        maxSum = arrSum;
    arrSum = 0;

for i in range(n): # 각 열의 합 최대 구하기
    for j in range(n):
        arrSum += arr[j][i];
    if maxSum < arrSum:
        maxSum = arrSum;
    arrSum = 0;

i = 0; # 인덱스
j = 0;
while i < n and j < n: # 하향 대각선 합 구한후 최대값과 비교
    arrSum += arr[i][j];
    if maxSum < arrSum:
        maxSum = arrSum;
    arrSum = 0;
    i += 1;
    j += 1;

i = 0            # 인덱스
j = n - 1;

while i < n and j > 0: # 상향 대각선 합 구하기
    arrSum += arr[i][j];
    if maxSum < arrSum:
        maxSum = arrSum;
    arrSum = 0;
    i += 1;
    j -= 1;    

print(maxSum)
```



## 문제 답안

```python
n = int(input());
a = [list(map(int, input().split())) for _ in range(n)]
largest= -2147000000 # 가장 작은 값으로 초기화
for i in range(n):
    sum1=sum2=0;
    for j in range(n): # 행, 열 합구하기
        sum1 += a[i][j]; # 행의 합
        sum2 += a[j][i]; # 열의 합
    if sum1 > largest:   # 최대값 입력
        largest = sum1;
    if sum > largest:
        largest = sum2;
sum1 = sum2 = 0
for i in range(n): # 두 대각선의 합 구하기
    sum1 += a[i][i];
    sum2 += a[i][n - i - 1];
    if sum1 > largest:   # 최대값 입력
        largest = sum1;
    if sum > largest:
        largest = sum2;
print(largest);
```



## 풀이와 답안 비교

답은 맞췄으나, 행과 열 각 대각선을 굳이 구분해서 구할 필요가 없었다. 코드를 짜기전에 어떻게 더 최적화 된 코드를 구성할 수 있을지 생각하는 습관이 필요할 것 같다.



# 2. 사과나무(다이아몬드)

## 문제 해설

* **슬라이싱을 응용한다.**



## 문제 풀이

```python
n = int(input());
arr = [list(map(int, input().split())) for _ in range(n)]; # 사과 농장 정보 받기
apple = 0;  # 수확한 사과
h = n // 2; # 슬라이싱 변수

i = 0; # index

while True:
    apple += sum(arr[i][h-i:h+1+i]);     # 다이아몬드를 반 나눴을 때 위의 수확량
    apple += sum(arr[n-1-i][h-i:h+1+i]); # 다이아몬드를 반 나웠을 때 아래의 수확량
    i += 1;
    if i == h:                         # 다이아몬드의 반 지점에서의 수확량
        apple += sum(arr[h][0:n]);
        break
print(apple);
```



## 문제 답안

```python
n = int(input());
a = [list(map(int, input().split())) for _ in range(n)];
res = 0;
s = e= n//2
for i in range(n):
    for j in range(s, e+1):
        res += a[i][j];
    if i < n//2:          # 다이아몬드의 반절 전
        s -=1
        e +=1
    else:                 # 다이아몬드의 반절 후
        s += 1;
        e -= 1;
```



## 풀이와 답안 비교

잘 푼것 같다! good! 다만, 변수를 정리할 필요가 있다.



# 3. 곶감(모래시계)

## 문제 해설

* **.pop()**: 리스트에서 해당 원소를 빼고 나머지 원소들을 앞으로 당긴다. 그 후 뺀 값을 return

## 문제 풀이

```python
import sys
sys.stdin = open("in5.txt", "rt")
n = int(input()); 
arr = [list(map(int, input().split())) for _ in range(n)]; # 2차원 배열 입력 받기
m = int(input());
for i in range(m):
    a, b, c = list(map(int, input().split())); # a: 행번호 b: 방향 c: 옮길 칸 수
    if c > n:
      c = c - n; # c가 n보다 긴 경우
    blnkArr =[] # 빈 배열 생성
    blnkArr = arr[a-1][0:n]; # 원래의 배열 담기
    if b == 0: # 왼쪽
        for j in range(n):
            arr[a-1][j-c] = blnkArr[j];
    else:      # 오른쪽
        for j in range(n):
            arr[a-1][j-n+c] = blnkArr[j];

gam = 0; # 감
s = 0;
e = n;

for i in range(n): # 모래시계 모양으로 세기
    for j in range(s, e):
        gam += arr[i][j];
    if i < n//2:
        s += 1;
        e -= 1;
    else:
        s -= 1;
        e += 1;
print(gam);
```



## 문제 답안

```python
n = int(input())
a = [list(map(int, input().split())) for _ in range(n)];
m = int(input())
for i in range(m):
    h, t, k = map(int, input().split());
    if t == 0: # 왼쪽
        for _ in range(k): # k만큼 회전
            a[h-1].append(a[h-1].pop(0)); # 1 번의 회전
    else: # 오른쪽
        for _ in range(k): # k만큼 회전
            a[h-1].insert(0, a[h-1].pop()); # 1 번의 회전 0 번 자리에 뺀 값을 넣기
            
res = 0;
s = 0;
e = n - 1;
for i in range(n):          # 모래시계 모양으로 감 더하기
    for j in range(s, e + 1):
        res += a[i][j];
    if i < n//2:
        s += 1;
        e -= 1;
    else:
        s -= 1;
        e += 1;           
```



## 풀이와 답안 비교

.pop이 뺀 뒤에 남은 리스트의 원소를 당기고 뺀 값을 return하는 것은 몰랐다. 그걸 감안해서 매우 잘 풀었다고 생각한다!



# 4. 봉우리

## 문제 해설

* **가장자리 0으로 감쌀 것**
* **방향 리스트(벡터) 사용하기**
  * **dx = [-1, 0, 1, 0];**
  * **dy = [0, 1, 0, -1];**
* **all()**
  * 안의 조건이 모두 참일 때 참

## 문제 풀이

```python
n =int(input());
map = [list(map(int, input().split())) for _ in range(n)];
map.insert(0, [0]*n); # 위에 0 추가
map.append([0]*n); # 아래에 0 추가
for x in map:     # 양옆에 0 추가
    x.insert(0, 0);
    x.append(0);

cnt = 0; # 봉우리 세기

for i in range(1, n+1): # 봉우리 탐색
    for j in range(1, n+1):
        if map[i][j] > map[i - 1][j]:
            if map[i][j] > map[i][j + 1]:
                if map[i][j] > map[i + 1][j]:
                    if map[i][j] > map[i][j - 1]:
                        cnt += 1;
print(cnt);
```



## 문제 답안

```python
dx = [-1, 0, 1, 0]; # 방향 리스트(벡터)
dy = [0, 1, 0, -1];
n =int(input());
a = [list(map(int, input().split())) for _ in range(n)];
a.insert(0, [0]*n); # 위에 0 추가
a.append([0]*n); # 아래에 0 추가
for x in a:     # 양옆에 0 추가
    x.insert(0, 0);
    x.append(0);
    
cnt = 0;
for i in range(1, n + 1):
    for j in range(1, n + 1):
        if all(a[i][j] > a[i+dx[k]][j+dy[k]] for k in range(4)): # 안의 조건이 모두 참일 때 참
            cnt += 1;
print(cnt);       
```



## 풀이와 답안 비교

방향 벡터와 리스트 테두리에 0 추가하는거 잘 기억해 놓자



# 5. 스도쿠 검사

## 문제 해설

* **3개의 체크리스트가 필요하다( 행, 열, 3*3)**
  * 각각 1 ~ 9까지 체크할 것 (있으면 1)

| 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
|      |      |      |      |      |      |      |      |      |

* **그룹(3 * 3)체크는 4중 for문이 필요하다.**

## 문제 풀이

```python
s = [list(map(int, input().split())) for _ in range(9)];
chR = list([0]*10); # 3개의 체크리스트
chC = list([0]*10);
chG = list([0]*10);
cnt = 0;            # 총 243이면 YES

for i in range(9): # 행과 열 체크
    for j in range(9):
        chR[s[i][j]] = 1;
        chC[s[j][i]] = 1;
    cnt += sum(chR);
    cnt += sum(chC);
    chR = list([0]*10); # 다시 0으로 초기화
    chC = list([0]*10);

a = 0;
b = 0;
for _ in range(0, 3): # 3*3 체크
    for _ in range(0, 3):
        for i in range(0 + a,3 + a):
            for j in range(0 + b, 3 + b):
                chG[s[i][j]] = 1;
        cnt += sum(chG);
        chG = list([0]*10);
        b += 3;
    b =0;
    a += 3;

print(cnt)
if cnt == 243:
    print("YES");
else:
    print("NO")
```



## 문제 답안

```python
def check(a):
    for i in range(9):
        ch1 = [0]*10;
        ch2 = [0]*10;
        for j in range(9):
            ch1[a[i][j]] = 1;
            ch2[a[j][i]] = 1;
        if sum(ch1)!=9 or sum(ch2)!=9:
            return False
    for i in range(3):              # 그룹탐색
        for j in range(3):
            ch3=[0]*10;
            for k in range(3):
                for s in range(3):
                    ch3[a[i*3+k][j*3+s]] = 1;
            if sum(ch3)!=9:
                return False
    return True

a = [list(map(int, input().split())) for _ in range(9)]
if check(a):
    print("YES");
else:
    print("NO");
```



## 풀이와 답안 비교

행과 열을 구하는 것은 어렵지 않았으나 그룹 탐색의 아이디어가 너무 생각이 안나서 살짝 힌트를 보고 풀었다. 4중 for문으로 잘 구현했으나, 채점할 때 전부 탐색할 필요가 없으니 return을 활용하자



# 6. 격자판 회문수

## 문제 해설

* **열은 리스트가 아니므로 슬라이싱이 안된다.**

## 문제 풀이

```python
g = [list(map(int, input().split())) for _ in range(7)];
cnt = 0; # 카운트
smallCnt = 0; # 2이면 카운트 1 증가
arrC=[];
for i in range(7):
    for j in range(3):
        arrR = g[i][0 + j:5 + j]; # 행 검사
        for k in range(2): # 회문 검사
            if arrR[k] == arrR[4 - k]:
                smallCnt += 1;
            if smallCnt == 2:
                cnt += 1;
        smallCnt = 0;
        for s in range(5):
            arrC.append(g[s+j][i]); # 열 검사
        for l in range(2): # 회문검사
            if arrC[l] == arrC[4 - l]:
                smallCnt += 1;
            if smallCnt == 2:
                cnt += 1;
        smallCnt = 0;
        arrC=[];
print(cnt);
```



## 문제 답안

```python
board = [list(map(int, input().split())) for _ in range(7)]
cnt = 0;
for i in range(3):
    for j in range(7): # 행 검사
        tmp = board[j][i:i+5];
        if tmp == tmp[::1]:
            cnt += 1;
        for k in range(2): # 열 검사
            if board[i + k][j]!= board[i + 5 - k - 1][j]:
                break
            else:
                cnt += 1;
print(cnt);
```



## 풀이와 답안 비교

열은 슬라이싱이 안된다! 기억하기. 열을 검사할 때, 리스트를 빼지말고 별개의 원소를 비교하자.