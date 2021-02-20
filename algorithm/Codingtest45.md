# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (26)(2021.2.19)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 토마토 (BFS)

## 문제 해설

* 토마토의 정보가 있는 2차원 배열(board), 익는데에 며칠 걸리는지 정보를 적는 2차원 배열(dis)을 만든다.
  * dis는 0으로 초기화
* board를 탐색하며 익은 토마토 정보를 큐에 넣기
* 상하좌우 탐색
* 익게된 토마토의 날짜를 기록
* 익게된 토마토를 큐에 넣기

## 문제 답안

```python
from collections import deque
dx = [-1, 0, 1, 0];
dy = [0, 1, 0, -1];
n, m = map(int, input().split());
board = [list(map(int, input().split())) for _ in range(m)]; # 토마토
Q = deque(); # 큐 자료구조
dis = [[0]*n for _ in range(m)]; # 익는 날짜
for i in range(m):
    for j in range(n):
        if board[i][j] == 1:
            Q.append((i, j)); # 튜플로 넣기
while Q:
    tmp = Q.popleft();
    for i in range(4): # 네 방향 탐색
        xx = tmp[0] + dx[i];
        yy = tmp[1] + dy[i];
        if 0 <= xx < m and 0 <= yy < n and board[xx][yy] == 0:
            board[xx][yy] = 1;
            dis[xx][yy] = dis[tmp[0]][tmp[1]] + 1; # 날짜 입력
            Q.append((xx, yy)); # 퍼져나가기
flag = 1;
for i in range(m):
    for j in range(n):
        if board[i][j] == 0: # 안 익은 토마토가 존재
            flag = 0;
result = 0;
if flag == 1:
    for i in range(m):
        for j in range(n):
            if dis[i][j] > result:
                result = dis[i][j];
    print(result);
else: # 안 익은 토마토 있을 때
    print(-1);
```



# 2. 사다리 타기(DFS)

## 문제 해설

* 도착지점의 열을 탐색해서 도착지로부터 출발지 역으로 탐색하기
* 별도의 체크 리스트를 만들 것

## 문제 풀이

```python
import sys
dx = [0, 0, -1]; # 3시, 9시, 12시
dy = [1, -1, 0];

def DFS(x, y):
    if x == 0: # 끝 도착 후 종료
        print(y);
        sys.exit(0);
    else:
        for j in range(3): # 세방향 탐색
            xx = x + dx[j];
            yy = y + dy[j];
            if 0 <= xx < 10 and 0 <= yy < 10 and board[xx][yy] == 1 and ch[xx][yy] == 0:
                  ch[xx][yy] = 1;
                  DFS(xx, yy);
                  ch[xx][yy] = 0;

if __name__ == "__main__":
    board = [list(map(int, input().split())) for _ in range(10)];
    ch = [[0]* 10 for _ in range(10)];
    for i in range(10): # 도착지
        if board[9][i] == 2:
            DFS(9, i);
```



## 문제 답안

```python
def DFS(x, y):
    ch[x][y] = 1;
    if x == 0: # 종착점
        print(y);
    else:
        if y -1 >= 0 and board[x][y-1] == 1 and ch[x][y - 1] == 0:
            DFS(x, y - 1); # 왼쪽
        elif y + 1 < 10 and board[x][y + 1] == 1 and ch[x][y + 1] == 0:
            DFS(x, y + 1); # 오른쪽
        else:
            DFS(x - 1, y); #  위쪽

if __name__ == "__main__":
    board = [list(map(int, input().split())) for _ in range(10)];
    ch = [[0]* 10 for _ in range(10)];
    for y in range(10):
        if board[9][y] == 2: # 타고 올라가기
            DFS(9, y);
```



## 풀이와 답안 비교

잘 풀었다.



# 3. 피자배달거리(DFS)

## 문제 해설

* 도시의 정보를 2차원 배열로 받아놓기
* 집의 좌표, 피자의 좌표를 각각 다른 리스트에 튜플 형태로 저장
* 총 피자집수에서 남길 피자집 수의 조합을 구하기

## 문제 답안

```python
def DFS(L, s):
    global res;
    if L == m:
        sum = 0; # 거리
        for j in range(len(hs)): # 집의 좌표
            x1 = hs[j][0];
            y1 = hs[j][1];
            dis = 2147000000;
            for x in cb: # 피자집의 좌표
                x2 = pz[x][0];
                y2 = pz[x][1];
                dis = min(dis, abs(x1 - x2) + abs(y1 - y2));
            sum += dis;
        if sum < res:
            res = sum;
    else:
        for i in range(s, len(pz)): # 피자집 조합 구하기
            cb[L] = i
            DFS(L + 1, i + 1)


if __name__ == "__main__":
    n, m = map(int, input().split()); 
    board = [list(map(int, input().split())) for _ in range(n)]; # 도시 정보
    hs = []; # 집
    pz = []; # 피자집
    cb = [0] * m; # 살아남는 피자집(조합의 경우)
    res = 2147000000; # 답
    for i in range(n): # 집, 피자집의 좌표 넣기
        for j in range(n):
            if board[i][j] == 1:
                hs.append((i, j));
            elif board[i][j] == 2:
                pz.append((i, j));
    DFS(0, 0);
    print(res);
```

