# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (24)(2021.2.17)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 동전 분배하기(DFS)

## 문제 해설

* **상태 트리**
  * 각 동전을 누구에게 주는지 정하기
  * 각 사람의 동전 금액을 기록하는 리스트 만들기

## 문제 답안

```python
def DFS(L):
    global res;
    if L == n: # 종료 지점
        cha = max(money) - min(money); # 최댓값과 최솟값의 차
        if cha < res:
            tmp = set() # set 자료구조
            for x in money:
                tmp.add(x);
            if len(tmp) == 3: # 서로 다 다른 금액
                res = cha;
    else:
        for i in range(3):
            money[i] += coin[L]; # 더하기
            DFS(L + 1);
            money[i] -= coin[L]; # 빠져왔을 때 다시 빼기

if __name__ == "__main__":
    n = int(input());
    coin = []; # 동전 리스트
    money = [0] * 3; # 각 사람이 가지고 있는 동전 금액 리스트
    res = 2147000000; # 차의 최소(답)
    for _ in range(n):
        coin.append(int(input()));
    DFS(0);
    print(res);
```



# 2. 알파코드(DFS)

## 문제 해설

* 상태 트리
  * 입력받은 숫자 리스트화
  * res(리스트)에 문자를 만들 숫자 집어 넣기
  * 26개의 문자 탐색
  * 한자리 숫자, 두자리 숫자 고려하기



## 문제 답안

```python
def DFS(L, P):
    global cnt;
    if L == n: # 종착점
        cnt += 1;
        for j in range(P):
            print(chr(res[j] + 64), end='');
        print();
    else:
        for i in range(1, 27): # 알파벳 뽑기
            if code[L] == i: # 한자리 숫자
                res[P] = i;
                DFS(L + 1, P + 1);
            elif i >= 10 and code[L] == i // 10 and code[L + 1] == i % 10: # 두자리 숫자
                res[P] = i;
                DFS(L + 2, P + 1);

if __name__ == "__main__":
    code = list(map(int, input())); # 받은 코드 리스트화
    n = len(code); # 길이(종착점)
    code.insert(n, -1); # out of index range 방지
    res = [0] * (n + 3);
    cnt = 0;
    DFS(0, 0);
    print(cnt);
```



# 3. 송아지 찾기(BFS: Breadth First Search)

## BFS

* 넓이 우선 탐색
* 레벨 탐색
* 큐 자료구조 사용
  * FIFO



## 문제 해설

* BFS 사용
* 거리 리스트 만들기
  * 체크 되어있으면 넘어가기
* 체크 리스트 만들기



## 문제 답안

```python
from collections import deque;

MAX = 10000;
ch = [0] * (MAX + 1); # 체크리스트
dis = [0] * (MAX + 1); # 거리
n, m = map(int, input().split()); # 현수, 송아지
ch[n] = 1; # 출발점 체크
dis[n] = 0; # 출발점
dQ = deque();
dQ.append(n);
while dQ:
    print(dQ)
    now = dQ.popleft() # 현재 지점
    if now == m: # 도착 지점
        break; 
    for next in(now - 1, now + 1, now + 5): # 다음위치 탐색
        if 0 < next <= MAX:  # 다음 위치가 음수가 아닐 때
            if ch[next] == 0: # 다음 위치가 방문한 곳이 아닐 때
                dQ.append(next); # 다음 위치 저장
                ch[next] = 1; # 방문 체크
                dis[next] = dis[now] + 1; # 이동횟수 해당 위치에 저장
print(dis[m]); # 도착지점일 때의 이동횟수(최솟값)
```



# 4. 사과나무(BFS)

## 문제 해설

* **상태 트리**
  * (n // 2,  n //2) 좌표로 시작점을 지정
  * 중심좌표를 중심으로 네방향을 탐색
  * 각 방향에서 방문한 곳을 제외하고 네방향을 탐색

## 문제 답안

```python
from collections import deque;

dx = [-1, 0, 1, 0];
dy = [0, 1, 0, -1];
n = int(input());
a = [list(map(int, input().split())) for _ in range(n)]; # 사과
ch = [[0] * n for _ in range(n)]; # 방문 여부 체크 리스트
sum = 0;
Q = deque();
ch[n//2][n // 2] = 1; # 중앙지점
sum += a[n // 2][n // 2]; # 중앙지점의 사과 갯수
Q.append((n // 2, n // 2)); # 중앙지점 넣기
L = 0
while True:
    if L == n // 2: # 목표지점
        break;
    size = len(Q) # size만큼 for문이 돈다.
    for i in range(size):
        tmp = Q.popleft();
        for j in range(4): # 퍼져 나가기
            x = tmp[0] + dx[j]; # x 좌표
            y = tmp[1] + dy[j]; # y 좌표
            if ch[x][y] == 0: # 방문하지 않은 곳일 때 합 누적
                sum += a[x][y];
                ch[x][y] = 1; # 방문 체크
                Q.append((x, y)); # 방문할 곳 저장
    L += 1;
print(sum);
```



# 5. 미로의 최단거리 통로(BFS)

## 문제 해설

* 최단 거리 문제 -> BFS 문제
* **상태 트리**
  * 각 위치에서 네방향 탐색
  * 체크리스트 만들기
  * 인덱스 번호가 0 ~ 6인 곳만 퍼져 나가기
  * 방문한 곳에 이동 거리 입력
  * 도착지는 (6, 6)좌표

## 문제 답안

```python
from collections import deque;

dx = [-1, 0, 1, 0]; # 네 방향 탐색
dy = [0, 1, 0, -1];
board = [list(map(int, input().split())) for _ in range(7)]; # 미로
dis = [[0] * 7 for _ in range(7)]; # 거리 기록
Q = deque();
Q.append((0, 0)); # 첫 번째
board[0][0] = 1; # 방문 한곳은 벽으로
while Q:
    tmp = Q.popleft();
    for i in range(4): # 탐색
        x = tmp[0] + dx[i]; # x 좌표
        y = tmp[1] + dy[i]; # y 좌표
        if 0 <= x <= 6 and 0 <= y <= 6 and board[x][y] == 0: # 벽이아니고 범위를 나가지 않을 때
            board[x][y] = 1; # 방문한 곳은 벽으로 만들기
            dis[x][y] = dis[tmp[0]][tmp[1]] + 1; # 거리 기록
            Q.append((x, y)); # 퍼져나갈 좌표
if dis[6][6] == 0: # 미로를 탈출하지 못한 경우
    print(-1);
else:
    print(dis[6][6]);
```



# Comment

BFS는 신세계다......... 복습해야겠다.