# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (31)(2021.2.24)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**

# 1. 플로이드 워샬 알고리즘

## 문제 해설

* 각 정점에서 각 정점으로의 최소 비용
  * 2차원 리스트
* 다이나믹 프로그래밍
  * 냅색 알고리즘
* dis[ i ] [ j ]: i노드에서 j노드로 가는데 드는 최소 비용
  * i: 출발점
  * j: 도착점
* i에서 j로 갈 때의 경우의 수
  * 이 중에서 최소비용을 찾기
* 최솟값을 찾기
  * dis[ i ] [ j ]
  * dis[ i ] [ k ] + dis[ k ] [ j ]
  * k: 중간 경유지 , for문으로 접근할 것
  * 비용이 제일 최소가 되는 순열로 이루어지게 된다.



## 문제 답안

```python
if __name__ == "__main__":
    n, m = map(int, input().split()); # 정점, 간선 개수
    dis =[[5000] * (n + 1) for _ in range(n + 1)]; # 간선 테이블
    for i in range(1, n + 1): # 자기자신으로가는 것은 0으로 초기화
        dis[i][i] = 0;
    for i in range(m):
        a, b, c = map(int, input().split()); # 인접행렬 만들기
        dis[a][b] = c;
    for k in range(1, n + 1): # 플로이드 워샬 알고리즘
        for i in range(1, n + 1):
            for j in range(1, n + 1):
                dis[i][j] = min(dis[i][j], dis[i][k] + dis[k][j]);
    for i in range(1, n + 1):
        for j in range(1, n + 1):
            if dis[i][j] == 5000:
                print("M", end = ' ');
            else:
                print(dis[i][j], end = ' ');
        print();
```

# 2. 회장뽑기 (플로이드 워샬 응용)

## 문제 해설

* 입력정보를 그래프화 (dis)
  * 강 행의 최댓값이 해당 행의 점수이다.
* 노드간의 최단거리 구하기
  * 노드간의 경로가 두 가지 이상인 경우, 최단거리가 가까움의 정도이다.
* 플로이드 워샬 (3중 for 문) 사용하기
* 1 차원 테이블(res)를 이용하여 각 회원들의 최대 점수를 기록한다.

## 문제 답안

```python
if __name__ == "__main__":
    n = int(input());
    dis = [[100] * (n + 1) for _ in range(n + 1)];
    for i in range(1, n + 1):
        dis[i][i] = 0; # 자기자신은 0
    while True:
        a, b = map(int, input().split());
        if a == -1 and b == -1:
            break
        dis[a][b] = 1; # 인접행렬
        dis[b][a] = 1;
    
    for k in range(1, n + 1): # 플로이드 와샬 , 각 회원의 점수 구하기
        for i in range(1, n + 1):
            for j in range(1, n + 1):
                dis[i][j] = min(dis[i][j], dis[i][k] + dis[k][j]);
   
    res = [0] * (n + 1);
    score = 100;
    for i in range(1, n + 1):
        for j in range(1, n + 1):
            res[i] = max(res[i], dis[i][j]) # 각 회원의 점수 기록
        score = min(score, res[i]);
    out = [];
    for i in range(1, n + 1):
        if res[i] == score:
            out.append(i); # 회장 후보 번호 넣기
    print("%d %d" %(score, len(out))); # 회장 후보 점수, 후보 수
    for x in out:
        print(x, end = ' ');
```



# 3. 위상 정렬 (그래프)

## 문제 해설

* **선후 관계를 유지하며 전체 일의 순서를 짜는 알고리즘**
* 방향 그래프
* **진입 차수** : 들어오는 간선의 수
  * 위상 정렬에서 중요
  * 1차원 리스트에 각 진입차수를 구하기
* 큐 자료구조 사용
  * 진입차수가 0인 것을 큐에 넣고 출력
  * 출력된 노드가 진입하는 곳의 진입 차수를 빼주기
  * 새롭게 0이 되는 노드를 큐에 넣기

## 문제 답안

```python
from collections import deque
n, m = map(int, input().split()); # 일의 개수, 순서
graph = [[0] * (n + 1) for _ in range(n + 1)]; # 인접행렬 0으로 초기화
degree = [0] * (n + 1); # 1차원 리스트(진입차수 계산)
dQ = deque(); # 큐 자료구조
for i in range(m):
    a, b = map(int, input().split()); 
    graph[a][b] = 1; # a -> b 
    degree[b] += 1; # b의 진입 차수
for i in range(1, n + 1):
    if degree[i] == 0:
        dQ.append(i); # 진입차수가 0인 노드 q 에 넣기

while dQ:
    x = dQ.popleft();
    print(x, end = ' '); # 빼기
    for i in range(1, n + 1): # 진입차수 0 탐색
        if graph[x][i] == 1:
            degree[i] -= 1;
            if degree[i] == 0:
                dQ.append(i);
```

