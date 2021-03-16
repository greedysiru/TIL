# [항해99 1기] [Chapter2-2] 자료구조, 알고리즘 (13) (2021.3.15)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**

# 1260

[문제 링크](https://www.acmicpc.net/problem/1260)

```python
# BFS를 사용하기위해 deque 가져오기
from collections import deque
# N: 정점의 개수 , M: 간선의 개수, V: 탐색을 시작할  정점의 번호
N, M, V = map(int, input().split())
# 간선의 개수만큼 입력 받기
# 인접 리스트를 받을 리스트 선언
G = [[] for _ in range(N + 1)]
# 입력받은 정보를 인접 리스트로 변환하기
for _ in range(M):
    a, b = map(int, input().split())
    G[a].append(b)
    G[b].append(a)
# 이차원 리스트의 각 리스트를 오름차순 정렬
for x in G:
    x.sort()
# DFS 정의
# 방문한 노드를 기록할 리스트
visit_array_dfs = []

def DFS(cur_node, adj_array, visit_array):
    # 현재 노드를 방문 배열에 기록
    visit_array.append(cur_node)
    # 방문한 노드를 출력
    print(cur_node, end=" ")
    # 인접 리스트에서 하나씩 탐색
    for adj_node in adj_array[cur_node]:
        # 현재 노드의 인접 노드가 방문 하지 않았으면
        if adj_node not in visit_array_dfs:
            # DFS 호출
            DFS(adj_node, adj_array, visit_array_dfs)

# 방문한 노드를 기록할 리스트
visit_array_bfs = []

def BFS(satart_node, adj_array):
    # 방문할 곳을 기록하는 큐를 출발하는 노드로 초기화
    visit_Q = [satart_node]
    visit_Q = deque(visit_Q)
    # 방문할 곳이 기록된 큐가 빌 때까지 반복
    while visit_Q:
        # 큐에 가장 먼저 들어온 노드를 현재 노드로 빼기
        cur_node = visit_Q.popleft()
        # 방문 리스트에 기록
        visit_array_bfs.append(cur_node)
        # 방문 노드 출력하기
        print(cur_node, end=" ")
        # 인접 노드 탐색
        for adj_node in adj_array[cur_node]:
            # 인접 노드가 방문하지 않았으면 큐에 추가
            if adj_node not in visit_array_bfs and adj_node not in visit_Q:
                visit_Q.append(adj_node)

DFS(V, G, visit_array_dfs)
print()
BFS(V, G)
```



## Comment

나는 받은 데이터를 인접리스트로 변환하였는데, 여기서 꼭 정렬을 해야 올바른 정답이 나온다.  로직자체가 맞아도 입력으로 값이 뒤죽박죽 들어오게 되면 답또한 틀려지기 때문이다.



# 2108

[문제 링크](https://www.acmicpc.net/problem/2108)

```python
# 산술평균 : N개의 수들의 합을 N으로 나눈 값
# 중앙값 : N개의 수들을 증가하는 순서로 나열했을 경우 그 중앙에 위치하는 값
# 최빈값 : N개의 수들 중 가장 많이 나타나는 값
# 범위 : N개의 수들 중 최댓값과 최솟값의 차이
import sys
from collections import Counter
# 수의 개수 N, N은 홀수
N = int(input())
# 수 입력 받기
num_array = []
for _ in range(N):
    num_array.append(int(sys.stdin.readline()))
# 중앙값을 구하기 위해서 오름차순 정렬
num_array.sort()
# 산술 평균
sum_array = sum(num_array)
# 반올림
print(round(sum_array / N))

# 중앙값
mid = N // 2
print(num_array[mid])

# 최빈값
# Counter 사용, 각 수의 빈도수를 dict로 만든다.
cnt_dict = Counter(num_array)
# .most_common()은 빈도수가 높은 순으로 튜플 형태로 정리 (수, 빈도수), 빈도수가 같으면 해당 수 기준 오름차순으로 정리된다.
cnt = cnt_dict.most_common()
# 하나 밖에 없는 경우
if len(cnt) == 1:
    print(cnt[0][0])
# 최빈값이 여러개인 경우 최빈값 중 두 번째로 작은 값 출력
elif cnt[0][1] == cnt[1][1]:
    print(cnt[1][0])
else:
    # 같지 않다면 최빈값 출력
    print(cnt[0][0])

# 범위
print(num_array[-1] - num_array[0])
```



## Comment

Counter를 사용하지 않으려 했으나 시간초과가 떠서 어쩔 수 없이 사용했다.



# 2630

[문제 링크]()

```python
# 종이 한 변의 길이 N
N = int(input())
# 전체 종이의 정보 입력 받기
P = []
for _ in range(N):
    P.append(list(map(int, input().split())))

# 하얀색 색종이의 개수
cnt_white = 0
# 파란색 색종이의 개수
cnt_blue = 0

# 종이를 이루는 총합을 구하는 함수
def total_paper(P, side):
    # 총합을 담을 변수
    sumP = 0
    for i in range(side):
        # 한 줄씩 더하기
        sumP += sum(P[i])
    # 리턴
    return sumP

# 종이가 같은 색으로 칠해져있는지 확인하는 함수
def check(P):
    global cnt_white
    global cnt_blue
    # 한변의 길이를 구하기
    side = len(P)
    # 주어진 종이를 이루는 총합 구하기
    sumP = total_paper(P, side)
    # 총합을 이용하여 종이를 체크
    # 총합이 0이면 전체 종이가 하얀색
    if sumP == 0:
        cnt_white += 1
    # 총합이 side ** 2 이면 전체 종이가 파란색
    elif sumP == (side ** 2):
        cnt_blue += 1
    # 총합이 위의 두 경우에 포함되지 않으면 종이가 섞여있으므로 나누어야 함
    else:
        divide(P, side)
    return

# 종이를 나누는 함수
def divide(P, side):
    # P를 4등분하여 p1, p2, p3, p4 만들기
    # 중간점
    mid = side // 2
    # 2차원 리스트 슬라이싱하기
    # 슬라이싱으로 전체에서 필요한 줄들을 가져와 for문으로 각 줄에 접근하여 슬라이싱을한다
    p1 = [row[:mid] for row in P[:mid]]
    p2 = [row[mid:] for row in P[:mid]]
    p3 = [row[:mid] for row in P[mid:]]
    p4 = [row[mid:] for row in P[mid:]]
    # 나누어진 부분별로 check함수 호출
    check(p1)
    check(p2)
    check(p3)
    check(p4)
    return

# 입력받은 종이부터 체크 -> 함수가 연결되어 작업
check(P)
# 하얀색 종이, 파란색 종이 출력하기
print(cnt_white)
print(cnt_blue)
```

## Comment

옛날부터 궁금했던 이차원 리스트의 슬라이싱을 터득했다! 코드 전체를 내가 스스로 만들어서 정답처리가 되었기에 뿌듯하다. (근데 정답률이 71프로나 되는 문제...)



# 15650

[문제 링크](https://www.acmicpc.net/problem/15650)

```python
def makeS(L):
    # 주어진 M만큼 수열을 만들게 되었을 때 출력
    if L == M:
        for i in range(L):
            # 나란히 출력
            print(S[i], end=" ")
        # 줄바꿈
        print()
    else:
        # 1부터 N까지의 수열 만들기
        for j in range(1, N + 1):
            # 해당 숫자를 사용하지 않은 경우
            if check[j] == 0:
                # 해당 수 이하를 체크하기
                for k in range(j + 1):
                    check[k] = 1
                # 수열에 숫자 넣기
                S[L] = j
                # 숫자 하나 고르기
                makeS(L + 1)
                # 돌아온 시점에서 다시 전부 초기화
                for l in range(j + 1):
                    check[l] = 0

# 자연수 N, M
# 1부터  N까지 자연수 중에서 중복 없이 M개를 고른 수열
# 고른 수열은 오름차순
N, M = map(int, input().split())
# 만들 수열을 담을 리스트
S = [0] * N
# 인덱스가 수열의 숫자를 표시하는 체크리스트 만들기
check = [0] * (N + 1)
# 수열을 만드는 깊이 우선 탐색 함수 호출
makeS(0)
```

## Comment

 오름차순만 만들어내는 것이 어려웠다.



# 9663

[문제 링크](https://www.acmicpc.net/problem/9663)

```python
# 퀸의 위치가 괜찮은지 확인하는 함수
# 괜찮으면 True
# 아니면 False
def check(L):
    # 입력된 곳까지 이전 말의 열 위치를 확인
    for j in range(L):
        # 현재 놓은 것과 이전에 놓은 것이 같으면 같은 열에 있는 것이므로 False
        # 이전과 다음의 열 차이가 1 이면 같은 대각선이므로 Flase
        if Q[j] == Q[L] or abs(Q[L] - Q[j]) == L - j:
            return False
    return True


# 퀸을 놓는 함수
# L: 놓아진 퀸의 행
def putQ(L):
    # 참조를 하기 위해서 cnt를 글로벌 변수 선언
    global cnt
    # 주어진 N만큼 퀸이 놓여지면 횟수 세기
    if L == N:
        cnt += 1
        return
    # 퀸 놓기
    else:
        # 각 행에 퀸 놓기
        # i는 열번호
        for i in range(N):
            Q[L] = i
            # 해당 위치가 괜찮은지 확인
            # True면 퀸 놓기 진행
            if check(L):
                putQ(L + 1)


# N x N인 체스판 위에 퀸 N개를 서로 공격할 수 없게 놓는 경우의 수 구하기
N = int(input())
# 퀸이 놓인 행이 인덱스이고 열이 그 값인 리스트 선언
# 0은 안 놓여있다는 표시
Q = [0] * N
# 경우의 수
cnt = 0
putQ(0)
print(cnt)
```



## Comment

파이썬3로는 시간초과가나와서 pypy3로 해야한다.

pypy3에서도 처음에는 시간초과가 나왔다. check 함수에서 이전과 다음의 열 차이를 별도에 변수에 넣었는데 그게 화근이었다. 변수 선언 조차도 시간복잡도에 영향을 주어서 그런 것 같다...



# 2579

[문제 링크](https://www.acmicpc.net/problem/2579)

```python
import sys
# 계단의 수
N = int(input())
# 계단 입력 받기
stair = [0] * N
for i in range(N):
    stair[i] = int(input())

# N이 1이면 계단이 하나이므로 그것을 바로 출력 후 종료
# N이 2이면 계단이 두개이므로 그것을 바로 출력 후 종료
if N == 1:
    print(stair[0])
    sys.exit(0)
elif N == 2:
    print(stair[0] + stair[1])
    sys.exit(0)
# 메모이제이션
# 각 위치에서의 최대 점수를 기록하기
# 0번 위치에서의 최댓값은 자기 자신
# 1번 위치에서 최댓값은 0번 위치와 1번 위치의 계단을 더한 값
# 2번 위치에서 최댓값은 0번 위치와 2번 위치의 계단을 더한 값과 1번 위치와 2번위치의 계단을 더한 값중 큰 값
memo = {
    0: stair[0],
    1: stair[0] + stair[1],
    2: max(stair[0] + stair[2], stair[1] + stair[2])
}

# 계단 점수 구하기
def score(N):
    # 메모이제이션이 된 값이라면 바로 해당 값 리턴
    if N in memo.keys():
        return memo[N]
    # 아닌 경우
    else:
        # N위치에서의 점수 점화식을 재귀적으로 표현
        # 두 가지의 경우
        # 1. 현위치에서 직전 계단을 밟은 경우
        # 2. 현위체에서 직접 계단을 밟지 않은 경우
        up1 = score(N - 3) + stair[N - 1] + stair[N]
        up2 = score(N - 2) + stair[N]
        memo[N] = max(up1, up2)
        return memo[N]

# 점수 출력하기
print(score(N - 1))
```



## Comment

점화식을 쓸 때 문제의 주어진 조건을 만족할 수 있도록 하자.



# 1002

[문제 링크](https://www.acmicpc.net/problem/1002)

```python
# 테스트 케이스 T
T = int(input())
# 좌표 입력 받기
for _ in range(T):
    x1, y1, r1, x2, y2, r2 = map(int, input().split())
    # 두 좌표 (x1, y1), (x2, y2)에서 r1, r2만큼 각각 떨어진 점은 각각의 좌표에서 r1, r2 만큼 떨어진 원의 경계선이다.
    # 그러므로 r1, r2는 각 원의 반지름
    # 각 좌표를 중심으로 하는 두 원의 위치관계를 이용해서 판별할 수 있음
    # 두 원의 중심 간 거리
    d = (((x1 - x2) ** 2) + ((y1 - y2) ** 2)) ** 0.5
    # 두 반지름 중 큰 것
    maxR = max(r1, r2)
    # 두 반지름 중 작은 것
    minR = min(r1, r2)
    # d == 0 인 조건을 우선적으로 볼 것
    # 동심원인 경우
    if d == 0 and maxR > minR:
        print(0)
    # 겹치는경우
    # 위치의 개수가 무한대
    elif d == 0 and maxR == minR:
        print(-1)
    # 두 점에서 만나는 경우
    # 두 원 서로 겹치는 것
    elif (maxR - minR) < d and d < (maxR + minR):
        print(2)
    # 한 점에서 만나는 경우
    # 두원이 한 점에서 겹치는 것
    # 외접
    elif maxR + minR == d:
        print(1)
    # 내접
    elif maxR - minR == d:
        print(1)
    # 만나지 않을 경우
    # 두 원이 외부로 떨어짐
    elif maxR + minR < d:
        print(0)
    # 두 원이 내부에서 만나지 않음
    elif maxR - minR > d:
        print(0)
```



# 2798

[문제 링크](https://www.acmicpc.net/problem/2798)

```python
# 조합을 사용하기 위한 itertools 가져오기
import itertools

# 카드의 개수 N, 목표로 하는 합 M
# M을 넘지 않아야 함
N, M = map(int, input().split())
# 카드 리스트 받기
card = list(map(int, input().split()))

# 최대합
res = 0

# 각 카드 조합의 합
sum_c = 0

# 카드 리스트에서 3개 뽑은 조합을 넣기
for cards in itertools.combinations(card, 3):
    # 카드 조합에서 카드 하나하나를 더하기
    for card in cards:
        sum_c += card
    # 합이 M이하이고 res보다 크면 res를 최신화
    if M >= sum_c and res < sum_c:
        res = sum_c
    # 다시 sum_c를 초기화
    sum_c = 0

print(res)
```



## Comment

itertools 라이브러리를 사용해서 카드 조합을 만들고 각 카드 조합의 합들을 구한 뒤 조건을 충족하는 것을 고르고 출력했다.



# 2231

[문제 링크](https://www.acmicpc.net/problem/2231)

```python
# 자연수  N의 가장 작은 생성자 구하기
N = int(input())
# 가장 작은 생성자 찾기
# 0부터 주어진 수까지 숫자 하나하나를 검사
for i in range(N + 1):
    # 문자열로 변환
    num_str = str(i)
    # 숫자의 길이
    length = len(num_str)
    # 분해합 구하기
    # 자기 자신으로 초기화
    num_sum = i
    # 자기 자신의 길이만큼 숫자 하나 하나 빼서 더하기
    for j in range(length):
        num_sum += int(num_str[j])
    # 분해합이 같으면 i가 생성자
    if N == num_sum:
        print(i)
        break
# 아니라면 0 출력
else:
    print(0)
```



## Comment

브루트포스로 작은수부터 생성자 조건에 맞는지 검사하였다.



# 1541

[문제 링크](https://www.acmicpc.net/problem/1541)

 ```python
# 식 입력 받기
# -기준으로 나누어 리스트로 받기
ex = input().split("-")


# ex리스트를 처음부터 끝까지 탐색
for i in range(len(ex)):
    # +가 있으면 그 위치인 양수가 리턴
    if ex[i].find("+") > 0:
        # +가 있는 문자열을 다시 + 기준으로 나누기
        sum_ex_arr = ex[i].split("+")
        # 합을 넣을 변수
        sum_ex = 0
        for j in range(len(sum_ex_arr)):
            # 숫자의 합 넣기
            sum_ex += int(sum_ex_arr[j])
        # 숫자의 합을 원래 자리에 넣어주기
        ex[i] = sum_ex

# 합을 적용한 리스트를 토대로 -연산을 실행
minus_ex = int(ex[0])
for k in range(1, len(ex)):
    # 1번 인덱스부터 뺄셈하기
    minus_ex -= int(ex[k])

# 답출력
print(minus_ex)
 ```



## Comment

입력 받은 식을 마이너스 기호 기준으로 slplit 하면 리스트 형태로 나누어진다. 그러면 각 요소는 숫자 또는 숫자와 플러스기호가 있는 상태이기 때문에 플러스 기호가 있는 부분을 각 숫자를 합해주고 최종적으로는 뺄셈 연산을 해준다.



# 11866

[문제 링크](https://www.acmicpc.net/problem/11866)

```python
# 큐 자료구조 사용
from collections import deque
# N: 사람수, K: 제거할 번호
N, K = map(int, input().split())
# 사람수만큼 리스트 생성후 큐로 변환
circle = deque([i for i in range(1, N + 1)])
# k번째가 아닐 때는 popleft를 하고 다시 append
# K번째는 popleft를 하고 그 요소를 별도의 리스트에 넣기
# 순서를 셀 i
i = 1
# 제거한 요소를 넣을 리스트
remove_arr = []
while circle:
    if i < K:
        # 뒤로 옮기기
        move = circle.popleft()
        circle.append(move)
        i += 1
    elif i == K:
        # 제거 리스트에 넣기
        remove = circle.popleft()
        remove_arr.append(remove)
        # i 초기화
        i = 1

print("<", end="")
print(*remove_arr, end="", sep=", ")
print(">", end="")
```



## Comment

while문과 별도의 변수를 사용하여 회전하는 효과를 넣어서 풀 수 있었다.



# 1992

[문제 링크](https://www.acmicpc.net/problem/1992)

```python
# 영상의 크기를 나타내는 숫자 N
N = int(input())
# 영상 정보 받기
V = [list(str(input())) for _ in range(N)]
# 문자열을 정수화
for row in range(N):
    V[row] = list(map(int, V[row]))

# 영상의 모든 요소의 합을 구하는 함수
def total_V(V, side):
    # 합을 저장할 변수 선언
    sum_V = 0
    # V의 각 줄의 합을 누적
    for row in range(side):
        sum_V += sum(V[row])
    # 구한 합을 리턴
    return sum_V

# 영상을 4개로 분할하는 함수
def div_V(V, side):
    # 나눴을 때 여는 괄호 출력
    print("(", end="")
    # 중간값
    mid = side // 2
    # 4개의 부분을 각각 이차원 슬라이싱
    v1 = [row[:mid] for row in V[:mid]]
    v2 = [row[mid:] for row in V[:mid]]
    v3 = [row[:mid] for row in V[mid:]]
    v4 = [row[mid:] for row in V[mid:]]
    # 나눈 부분으로 다시 check_V 함수 호출
    check_V(v1)
    check_V(v2)
    check_V(v3)
    check_V(v4)
    # 나누고 나서 닫는 괄호 출력
    print(")", end="")
    return

# 영상 정보가 0이나 1로만 되어있는 지 체크하는 함수
def check_V(V):
    # 영상 한 변의 길이
    side = len(V)
    # 영상의 모든 요소의 합 구하기
    sum_V = total_V(V, side)
    # sum_V가 적절한 값인지 판별
    # 모든 값이 0이라면 그 총합도 0이므로 0을 print
    if sum_V == 0:
        print(0, end="")
    # 모든 값이 1이라면 그 총합이 변의 제곱이므로 1을 print
    elif sum_V == (side ** 2):
        print(1, end="")
    else:
        # 위의 조건에 맞지 않으면 0과 1이 섞여있는 것이므로 4개로 분할
        div_V(V, side)
    return

# V를 호출
check_V(V)
```



## Comment

2630 종이문제와 거의 똑같은 문제. 단, 괄호를 출력할 때 적절한 부분을 찾는 것이 조금 헷깔렸으나 함수의 호출 순서를 잘 생각하면 찾아낼 수 있었다.