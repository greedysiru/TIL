# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (25)(2021.2.18)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 미로탐색(DFS)

## 문제 해설

* **방법의 수를 구하는 것에 유의 -> DFS**
* 지나온 길은 재방문하지 않는다.
* 경로를 탐색 후 지나온 길의 체크를 풀 것

## 문제 답안

```python
dx = [-1, 0, 1, 0]; # 방향
dy = [0, 1, 0, -1];
def DFS(x, y):
    global cnt;
    if x == 6 and y == 6: # 도착지점
        cnt += 1;
    else:
        for i in range(4):
            xx = x + dx[i]; # 갈 곳
            yy = y + dy[i];
            if 0 <= xx <= 6 and 0 <= yy <= 6 and board[xx][yy] == 0:
                board[xx][yy] = 1; # 체크
                DFS(xx, yy);
                board[xx][yy] = 0; # 체크 풀기

if __name__ == "__main__":
    board = [list(map(int, input().split())) for _ in range(7)];
    cnt = 0;
    board[0][0] = 1; # 출발점 체크
    DFS(0, 0);
    print(cnt);        
```



# 2.  등산경로(DFS)



## 문제 해설

* 출발점, 도착점이 입력에 따라 달라진다.
* 이동 시, 자신보다 높은 값으로만 이동이 가능하다.
* 이동 경로를 체크하며 탐색
* 되돌아오면, 체크를 풀기

## 문제 풀이

```python
dx = [-1, 0, 1, 0]; # 방향
dy = [0, 1, 0, -1];

def DFS(x, y):
    global cnt;
    if m[x][y] == end: # 도착지
        cnt += 1;

    else:
        for i in range(4):
            xx = x + dx[i];  # 갈 좌표 값
            yy = y + dy[i];
            if 0 <= xx < n and 0 <= yy < n and ch[xx][yy] == 0:
                if m[x][y] < m[xx][yy]: # 더 높은 구역
                    ch[xx][yy] = 1;
                    DFS(xx, yy);
                    ch[xx][yy] = 0;

if __name__ == "__main__":
    n = int(input());
    m = [list(map(int, input().split())) for _ in range(n)];
    ch = [[0]* n for _ in range(n)];
    start = 200;
    end = 0;
    for i in range(n):
        for j in range(n):
            if start > m[i][j]:
                start = m[i][j];
            if end < m[i][j]:
                end = m[i][j];
    cnt = 0; # 카운트
    for i in range(n):
        for j in range(n):
            if start == m[i][j]:
                ch[i][j];
                DFS(i, j);
    print(cnt);
```



## 문제 답안

```python
dx = [-1, 0, 1, 0]; # 방향
dy = [0, 1, 0, -1];

def DFS(x, y):
    global cnt;
    if x == ex and y == ey: # 도착지점
        cnt += 1;
    else:
        for k in range(4):
            xx = x + dx[k];
            yy = y + dy[k];
            if 0 <= xx < n and 0 <= yy < n and ch[xx][yy] == 0 and board[xx][yy] > board[x][y]:
                ch[xx][yy] = 1;
                DFS(xx, yy);
                ch[xx][yy] = 0;

if __name__ == "__main__":
    n = int(input()); # 지도의 크기
    board = [[0] * n for _ in range(n)]; # 지도 정보 초기화
    ch = [[0] * n for _ in range(n)]; # 체크 리스트
    max = - 2147000000; # 최댓값
    min = 2147000000; # 최솟값
    for i in range(n): # 입력 받으며 최솟값, 최댓값 탐색
        tmp = list(map(int, input().split()));
        for j in range(n):
            if tmp[j] < min: # 최솟값
                min = tmp[j];
                sx = i;
                sy = j;
            if tmp[j] > max: # 최댓값
                max = tmp[j];
                ex = i;
                ey = j;
            board[i][j] = tmp[j];
    ch[sx][sy] = 1; # 출발 지점
    cnt = 0;
    DFS(sx, sy);
    print(cnt);
```



## 풀이와 답안 비교

내 코드는 for문을 너무 남발했다.



# 3. 단지 번호 붙이기(DFS)

## 문제 해설

* 이중  for문이 돌며 단지를 탐색
  * 1을 발견하면 DFS를 호출해서 집 개수를 카운팅하기
  * 답을 위한 리스트에 찾은 집 개수 넣기
  * 단지 개수, 집 개수를 출력
* 방문한 집은 0으로 체크
* BFS로도 탐색 가능

## 문제 답안

```python
dx = [-1, 0, 1, 0]; # 방향
dy = [0, 1, 0, -1];

def DFS(x, y):
    global cnt;
    cnt += 1; # 집 카운팅
    board[x][y] = 0; # 방문 체크
    for i in range(4): # 네방향
        xx = x + dx[i];
        yy = y + dy[i];
        if 0 <= xx < n and 0 <= yy < n and board[xx][yy] == 1:
            DFS(xx, yy);

if __name__ == "__main__":
    n = int(input());
    board = [list(map(int, input())) for _ in range(n)];
    res = []; # 집, 단지
    for i in range(n):
        for j in range(n): # 집 탐색
              if board[i][j] == 1: # 집 발견
                  cnt = 0; # 매 단지마다의 집의 개수
                  DFS(i, j);
                  res.append(cnt); # 단지 집 개수 저장
    print(len(res)); # 단지의 개수
    res.sort(); # 오름차순 정렬
    for x in res: # 단지 출력
        print(x);
```



# 4. 섬나라 아일랜드(BFS)

## 문제 해설

* 8방향 탐색
* 섬이 몇개 있는지만 갯수를 센다.



## 문제 답안

```python
from collections import deque

dx = [-1, -1, 0, 1, 1, 1, 0, -1]; # 8 방향
dy = [0, 1, 1, 1, 0, -1, -1, -1];
n = int(input()); # 격자 크기
board = [list(map(int, input().split())) for _ in range(n)]; # 지도 정보
cnt = 0; # 섬 카운트
Q = deque(); # 큐 자료구조

for i in range(n):
    for j in range(n):
        if board[i][j] == 1:
            board[i][j] = 0; # 체크
            Q.append((i, j)); # 좌표 넣기
            while Q:
                tmp = Q.popleft();
                for k in range(8): # 8방향 탐색
                    x = tmp[0] + dx[k];
                    y = tmp[1] + dy[k];
                    if 0 <= x < n and 0 <= y < n and board[x][y] == 1:
                        board[x][y] = 0; # 체크
                        Q.append((x, y));
            cnt += 1;
print(cnt);
```



# 5. 안전영역(BFS)

## 문제 해설

* DFS로도 가능
* 체크 리스트 만들기 (2차원 리스트)
* 강수량에 따라 안 잠기는 지역 구하기

## 문제 답안

```python
import sys
sys.setrecursionlimit(10**6); # 10**6 넘으면 재귀함수 종료
dx = [-1, 0, 1, 0];
dy = [0, 1, 0, -1];

def DFS(x, y, h):
    ch[x][y] = 1; # 방문
    for i in range(4): # 4방향 탐색
        xx = x + dx[i];
        yy = y + dy[i];
        # 경계를 넘지 않고 물에 잠기지 않은 미방문 지역
        if 0 <= xx < n and 0 <= yy < n and ch[xx][yy] == 0 and board[xx][yy] > h:
            DFS(xx, yy, h);

if __name__ == "__main__":
    n = int(input()); # 지도 크기
    res = 0; # 최종 답
    board = [list(map(int, input().split())) for _ in range(n)]; # 지도 정보
    for h in range(100): # 0 ~ 99
        ch = [[0] * n for _ in range(n)]; # 체크리스트
        cnt = 0;
        for i in range(n): # 탐색
            for j in range(n):
                if ch[i][j] == 0 and board[i][j] > h: # 물에 잠기지 않는 지점
                    cnt += 1; # 안전영역
                    DFS(i, j, h);
        res = max(res, cnt) # 최댓값 입력
        if cnt == 0: # 안전영역을 더 이상 발견 못하면 중단
            break;
    print(res);
```

