# [항해99 1기] [Chapter2-1] 자료구조, 알고리즘 (9) (2021.3.11)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**



# 2606

[문제 링크](https://www.acmicpc.net/problem/2606)

```python
# 컴퓨터의 수
n = int(input())
#  네트워크 상에서 직접 연결되어 있는 컴퓨터 쌍의 수
c = int(input())
# 감염 여부 체크
infested = []
# 인접한 컴퓨터 딕셔너리
computer = {}
for i in range(1, n + 1):
    computer[i] = []
# 입력 받기
for _ in range(c):
    # a: 감염된 컴퓨터 b: 인접 컴퓨터
    a, b = map(int, input().split())
    computer[a].append(b)
    computer[b].append(a)

# DFS 선언
def DFS(computer, cur_com, infested):
    # 감염 체크
    infested.append(cur_com)
    # 인접 컴퓨터 감염
    # 현재 컴퓨터가 키로 있을 경우
    if cur_com in computer:
        # 해당하는 키의 값들을 탐색
        for ad_com in computer[cur_com]:
            # 감염체크가 안되어 있는 경우
            if ad_com not in infested:
                DFS(computer, ad_com, infested)
    return

DFS(computer, 1, infested)
# 1번 컴퓨터는 제외이므로 1을 뺀다.
print(len(infested) - 1)
```



## Comment

처음에 입력값을 그래프로 만들지 않았는데 예제는 통과했지만 테스트 케이스에서는 오답처리가 되었다. 그래서 올바른 그래프를 만들고 다시 채점하니 정답처리가 되었다.



# 7576

[문제 링크](https://www.acmicpc.net/problem/7576)

```python
from collections import deque

# 상자의 크기
m, n = map(int, input().split())
# 토마토 상자 정보 입력 받기
box = [list(map(int, input().split())) for _ in range(n)]
# 좌표 이동
# 상, 하
dx = [-1, 0, 1, 0]
# 좌, 우
dy = [0, -1, 0, 1]
# 각 자리의 토마토가 익은 날짜를 입력할 이차원 리스트
check = [[0] * m for _ in range(n)]

# 익은 토마토가 있는 인덱스 찾기
tomatoIndex = []
for i in range(n):
    for j in range(m):
        # 익은 토마토 위치를 찾아 tomatoIndex에 저장
        if box[i][j] == 1:
            tomatoIndex.append([i, j])
# 큐 자료형 변환
tomatoIndex = deque(tomatoIndex)
# 찾은 토마토 위치로 익은 토마토 일수 계산하기
while tomatoIndex:
    # tomatoIndex에 있는 가장 처음에 있던 인덱스 추출
    curIndex = tomatoIndex.popleft()
    # 네 방향 탐색
    for i in range(4):
        xx = curIndex[0] + dx[i]
        yy = curIndex[1] + dy[i]
        # 이동하는 곳이 경계선을 넘지 않고 토마토가 익지 않은 곳이면 아래 명령 실행
        if 0 <= xx < n and 0 <= yy < m and box[xx][yy] == 0:
            # 익었다는 표시
            box[xx][yy] = 1
            # 체크 배열에는 익은 일자를 표시, 전 위치에 표시된 일자에 + 1
            check[xx][yy] = check[curIndex[0]][curIndex[1]] + 1
            # 퍼져나가기 위해 tomatoIndex에 추가하기
            tomatoIndex.append([xx, yy])

# 안 익은 토마토 확인
flag = False
# 토마토 익은 최소 일수를 담을 변수
day = 0
for i in range(n):
    for j in range(m):
        # 안 익은 토마토가 있는 경우
        if box[i][j] == 0:
            flag = True
            break
        # 체크 배열에서 가장 최대의 값을 찾기
        if day < check[i][j]:
            day = check[i][j]

if flag:
    print(-1)
else:
    print(day)
```



# Comment

악명 높은 그 야채 문제.... 그래도 전에 공부한 유형과 비슷해서 어찌저찌 풀었다. 큐를 안쓰고 pop(0)을 썻을 때는 시간초과가 나왔지만 큐를 쓰고 popleft()를 사용하니 통과.



# 1003

[문제 링크](https://www.acmicpc.net/problem/1003)

```python
# 테스트 케이스
t = int(input())

# 메모이제이션
memo = {0: [1, 0], 1: [0, 1]}


def fibo(n, memo):
    # 0과 1이 호출된 경우
    if n in memo:
        return memo[n]
    # 없는 경우
    for i in range(2, n + 1):
        cntZero = memo[i - 2][0] + memo[i - 1][0]
        cntOne = memo[i - 2][1] + memo[i - 1][1]
        count = [cntZero, cntOne]
        memo[i] = count
    return memo[n]


for _ in range(t):
    # 0과 1의 호출 배열
    cntArr = fibo(int(input()), memo)
    print(cntArr[0], end=" ")
    print(cntArr[1])

```

## Comment

오기로 내 방식으로 풀어버렸다...



# 11053

[문제 링크](https://www.acmicpc.net/problem/11053)

```python
n = int(input())
arr = list(map(int, input().split()))
arr.insert(0, 0)
# 1번 ~n번 리스트
dy = [0] * (n + 1)
# 각 인덱스에서의 부분수열 길이
dy[1] = 1
# 첫번째 인덱스의 부분 수열 길이
res = 0
# 답
for i in range(2, n + 1):  # 각 인덱스 부분 수열 길이 구하기
    max = 0
    for j in range(i - 1, 0, -1):  # i번째 인덱스 앞 탐색
        if arr[j] < arr[i] and dy[j] > max:
            max = dy[j]
    dy[i] = max + 1
    if dy[i] > res:
        res = dy[i]
print(res)
print(dy)
```

 

## Comment

전에 풀었는데 잊어버려서 다시 공부했다.