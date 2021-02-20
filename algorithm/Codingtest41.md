# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (22)(2021.2.15)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 조합 구하기(DFS)

* **매우 중요!**

## 문제 해설

* **매개변수를 두 개로 할 것**
  * D(L, s)
  * s : 가지가 뻗기 시작하는 번호




## 문제 답안

```python
def DFS(L, s):
    global cnt;
    if L == m:
        for j in range(L):
            print(res[j], end=" ");
        cnt +=1;
        print();
    else:
        for i in range(s, n + 1):
            res[L] = i;
            DFS(L + 1, i + 1);    

if __name__ == "__main__":
    n, m = map(int, input().split());
    res = [0] * (n + 1); # 조합을 넣을 리스트
    cnt = 0; # 카운트
    DFS(0, 1);
    print(cnt);
```

* DFS를 호출하는 곳에서 막혔다. s에 더하는 것이 아닌, **i에 더해야 적절한 상태트리가 만들어진다.**



# 2. 수들의 조합(DFS)

## 문제 해설

* 부분집합을 만들어낸다.
  * 각 부분집합의 합을 구하기
* DFS(L, s, sum) 
  * L: 레벨
  * s: for문이 시작하는 곳
  * sum: 합계

## 문제 풀이

```python
def DFS(L, s, sum): # 레벨, for문이 시작하는 곳, 합
    global cnt;
    if L == k: # 종료 지점
        if (sum % m) == 0: # 주어진 수의 배수인 경우
            cnt += 1;
        return;
    else:
        for i in range(s, n):
          DFS(L + 1, i + 1, sum + a[i]);


if __name__ == "__main__":
    n, k = map(int, input().split());
    a = list(map(int, input().split()));
    m = int(input());
    cnt = 0; # 카운트
    DFS(0, 0, 0);
    print(cnt);
```



## 문제 답안

```python
def DFS(L, s, sum):
    global cnt;
    if L == k:
        if sum % m == 0:
            cnt += 1;
    else:
        for i in range(s, n):
            DFS(L + 1, i + 1, sum + a[i]);

if __name__ == "__main__":
    n, k = map(int, input().split());
    a = list(map(int, input().split()));
    m = int(input());
    cnt = 0; # 카운트
    DFS(0, 0, 0);
    print(cnt);
```



## 풀이와 답안 비교

많이 참고하긴 했지만 잘 풀었다.



# 3. 라이브러리를 이용한 순열(수열 추측하기)

* 이전의 수열 추측하기 문제를 파이썬의 **itertools 라이브러리**를 사용하여 풀어본다. (파이썬 알고리즘 문제 풀이(21))
  * **itertools** : 순열, 조합을 구할 수 있다.
* **코딩테스트에 라이브러리의 남발은 자제하는 것이 좋다.**
  * 테스트 별로 제한하는 경우가 있음



## itertools

```python
import itertools as it
n, f = map(int, input().split());
b = [1] * n;
for i in range(1, n):
    b[i] = b[i - 1] * (n - i)/ i; # 이항계수
a = list(range(1, n + 1));
for tmp in it.permutations(a): # a의 자료를 순열로 구한다. 튜플형태로 tmp에 저장
   print(tmp);
```

* **permutations():** 입력한 자료의 순열 구한다. 자료형 다음에 숫자를 입력하면 그만큼 뽑은 경우의 순열을 구한다.



## itertools를 이용한 문제 답안

```python
import itertools as it
n, f = map(int, input().split());
b = [1] * n;
for i in range(1, n):
    b[i] = b[i - 1] * (n - i)/ i; # 이항계수
a = list(range(1, n + 1));
for tmp in it.permutations(a): # a의 자료를 순열로 구한다. 튜플형태로 tmp에 저장
    sum = 0;
    for L, x in enumerate(tmp): # tmp의 인덱스와 값 뽑아내기
        sum += (x * b[L]); # 이항계수와 곱한 뒤 sum에 더하기
    if sum == f:
        for x in tmp:
            print(x, end = " ");
        break;
```



# 4. 라이브러리를 이용한 수들의 조합

* 2번 문제를 **itertools 라이브러리**를 이용하여 풀어본다.



## itertools를 이용한 문제 답안

```python
import itertools as it
n, k = map(int, input().split());
a = list(map(int, input().split()));
m = int(input());
cnt = 0; # 카운트
for x in it.combinations(a, k): # a리스트에서 k개를 뽑은 조합을 x에 넣기
    if sum(x) % m == 0:
        cnt += 1;
print(cnt);
```



# 5. 인접행렬(가중치 방향 그래프)

## 그래프의 종류

* **그래프 : 노드와 간선의 집합**
* **방향** 그래프 : **간선의 방향이 설정**되어 있는 그래프
* **가중치** 방향 그래프 : 간선의 뱡향과 **값이 설정**되어 있는 그래프



## 그래프의 구현 (기본)

* **이차원 리스트**를 이용하여 구현
* 행번호, 열번호 == 노드 번호
* 행 번호에서 출발하여 열 번호에 도착한다.
  * 1번노드와 2번노드가 연결되어 있는 경우
  * **1번 행과 2번 열을 찾아서 1을 입력**
  * 2번노드에서 1번노드로 갈 수도 있으므로
  * **2번 행과 1번 열을 찾아서 1을 입력**



### 코드 구현

```python
n, m = map(int, input().split());
g = [[0] * (n + 1) for _ in range(n + 1)]; # 인접행렬 그래프

for i in range(m): # 간선 정보 받기
  a, b = map(int, input().split());
  g[a][b] = 1; # 인접행렬 체크
  g[b][a] = 1;

for i in range(1, n + 1):
    for j in range(1, n + 1):
        print(g[i][j], end = " ");
    print();
```



## 가중치 방향 그래프의 구현

* **방향을 고려하여 입력**
* **간선의 가중치를 해당 열번호와 행번호에 입력**



## 문제 풀이

```python
n, m = map(int, input().split());
g = [[0] * (n + 1) for _ in range(n + 1)]; # 그래프

for i in range(m): # 간선 정보 받기
  a, b, c = map(int, input().split()); # c는 거리비용
  g[a][b] = c;

for i in range(1, n + 1):
    for j in range(1, n + 1):
        print(g[i][j], end = " ");
    print();
```



# 6. 경로탐색 (그래프 DFS)

## 문제 해설

* 상태 트리
  * 각 노드에서 갈 수 있는 노드를 탐색
  * for문
* 한 번 방문한 노드는 다시 방문하지 못한다.
  * **체크리스트 만들 것**



## 문제 답안

```python
def DFS(v): # 노드번호
    global cnt;
    if v == n: # 종착지점
        cnt += 1;
    else:
        for i in range(1, n + 1):
              if g[v][i] == 1 and ch[i] == 0:
                  ch[i] = 1;
                  DFS(i)
                  ch[i] = 0; # 체크 풀기                          

if __name__ == "__main__":
    n, m = map(int, input().split()); # 정점, 간선의 수
    g = [[0] * (n + 1) for _ in range(n + 1)];
    ch = [0] * (n + 1); # 체크리스트
    for i in range(m): # 연결정보 받기
        a, b = map(int, input().split());
        g[a][b] = 1;
    cnt = 0; # 카운트
    ch[1] = 1
    DFS(1);
    print(cnt);
```

