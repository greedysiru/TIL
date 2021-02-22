# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (29)(2021.2.22)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 1. 알리바바와 40인의 도둑(Bottom-Up)

## 문제 해설

* 최단거리로 가기위해서는 **오른쪽, 아래**로 움직인다.
* 별도의 dy 2차원 리스트 만들기
  * 출발지에서 각 지점까지 가는데 드는 **최소 비용**
  * 0행과 0열의 dy 값은 **누적되어 가는 값**이다.

## 문제 풀이

```python
n = int(input());
a = [list(map(int, input().split())) for _ in range(n)];
dy = [[0]*n for _ in range(n)]; # 각 지점에서의 최소 비용
dy[0][0] = a[0][0]; # 시작점

for i in range(1 , n): # dy의 0행, 0열 초기화
    dy[0][i] = a[0][i] + dy[0][i - 1];
    dy[i][0] = a[i][0] + dy[i - 1][0];

for i in range(1, n):
    for j in range(1, n):
        if dy[i - 1][j] > dy[i][j - 1]:
            dy[i][j] = a[i][j] + dy[i][j - 1];
        else:
            dy[i][j] = a[i][j] + dy[i - 1][j];
print(dy[n -1][n - 1]);
```



## 문제 답안

```python
if __name__ == "__main__":
    n = int(input());
    arr = [list(map(int, input().split())) for _ in range(n)];
    dy = [[0] * n for _ in range(n)]; # dy 테이블
    dy[0][0] = arr[0][0]; # 초기화
    for i in range(n): # dy 0행, 0열 초기화
        dy[0][i] = dy[0][i - 1] + arr[0][i];
        dy[i][0] = dy[i - 1][0] + arr[i][0];
    
    for i in range(1, n):
        for j in range(1, n):
            dy[i][j] = min(dy[i - 1][j], dy[i][j - 1]) + arr[i][j];

print(dy[n - 1][n- 1]);
```



## 풀이와 답안 비교

잘 풀었다! 다만, min함수를 쓰는게 나았다.

# 2. 알리바바와 40인의 도둑 (Top-Down)

## 문제 해설

* 재귀함수
* **상태 트리**
  * DFS(n, n): n,n 좌표까지 오는데 드는 최소 에너지 비용
  * 이동은 오른쪽 또는 아래로만 가능
  * DFS(n, n)는 DFS(n, n - 1), DFS(n - 1, n)에서 작은 값으로과 자신의 자리의 에너지비용을 합한 값
  * 이미 호출되었던 함수는 메모이제이션 한다.
  * dy에 메모이제이션 할 것
  * 좌표를 넘지 않도록 한다.



## 문제 풀이

```python
def DFS(x, y):
    if dy[x][y] > 0: # 이미 호출된 경우
        return dy[x][y];
    if x == 0 and y == 0:
        return arr[0][0] # 시작점의 에너지 비용
    else:
        if y == 0:
            dy[x][y] = DFS(x - 1, y) + arr[x][y]
        elif x == 0:
            dy[x][y] = DFS(x, y - 1) + arr[x][y];
        else: # 위와 왼쪽 중 작은 값과 더하기
            dy[x][y] = min(DFS(x - 1, y), DFS(x, y - 1)) + arr[x][y];
        return dy[x][y];


if __name__ == "__main__":
    n = int(input());
    arr = [list(map(int, input().split())) for _ in range(n)];
    dy = [[0] * n for _ in range(n)]; # 메모이제이션
    print(DFS(n - 1, n - 1)); # 도착지점
```



