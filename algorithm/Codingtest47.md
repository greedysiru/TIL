# [인프런 - 김태원] 파이썬 알고리즘 문제풀이 (코딩테스트 대비) (28)(2021.2.21)



**본 내용은 해당 [강의](https://www.inflearn.com/course/파이썬-알고리즘-문제풀이-코딩테스트/dashboard) 토대로 작성**



# 동적계획법

* Dynamic Programming
* 크고 복잡한 문제를 다룰 때 문제를 직관적인 작은 단위로 바꾸어 해를 구한다.
* 그 후, 조금 더 큰 문제로 확장하여 구한 해를 이용하여 조금 더 큰 문제의 해를 구한다.
* 이 구한 작은 단위들의 해들은 따로 기록한다**(메모이제이션)**
* 이를 반복하여 주어진 문제의 점화식을 도출해서 답을 구한다.
* **바텀업 방식**



# 1. 네트워크 선 자르기(Bottom- Up, Top-Down)

## 문제 해설(Bottom-Up)

* 1미터부터 방법의 수를 기록하여 **점화식 구하기**
  * 1미터 -> 1
  * 2미터 -> 2
  * 3미터 -> 3
  * 4미터 -> 5
  * **점화식: f(n) = f(n - 2) + f(n - 1)**



## 문제 답안(Bottom-Up)

```python
n = int(input());
dy = [0] * (n + 1); # 1번부터 해당 번호까지
dy[1] = 1;
dy[2] = 2; # 직관적인 해
for i in range(3, n + 1): # 문제의 해 구하기
    dy[i] = dy[i - 1] + dy[i - 2];
print(dy[n]);
```



## 문제 해설(Top-Down)

* 탑다운 방식으로 풀기
* DFS(n) : n미터 길이의 선을 자르는 경우의 수를 리턴
* 이미 구한 해는 테이블에 기록(메모이제이션)
* 재호출된 함수는 메모이제이션한 값을 리턴하여 불필요한 재귀함수 호출 방지



## 문제 답안(Top-Down)

```python
def DFS(len):
  if dy[len] > 0: # 이미 호출된 함수의 경우
    return dy[len]
  if len == 1 or len == 2: # 1, 2의 경우
      return len
  else:
      dy[len] = DFS(len - 1) + DFS(len - 2);
      return dy[len]

if __name__ == "__main__":
    n = int(input());
    dy = [0] * (n + 1); # 메모이제이션
    print(DFS(n))
```



# 2. 도전과제 : 계단오르기(Top-Down : 메모이제이션)



## 문제 해설

* **탑다운** 
* 메모이제이션, 재귀함수 사용
* DFS(n) : n번째 계단에 가기위한 방법의 수



## 문제 답안

```python
n= int(input());
dy = [0]*(n + 2); # n개의 돌다리와 건너편
dy[1] = 1; # 첫 번째와 두 번째 돌다리의 방법의 수
dy[2] = 2;
for i in range(3, n + 2):
    dy[i] = dy[i - 1] + dy[i - 2];

print(dy)
print(dy[n + 1]);
```



# 3. 최대 부분 증가 수열 (LIS : Longest Increasing Subsequence)

## 문제 해설

* **바텀업 (DP)**
* 주어진 수열을 작게 쪼개서 부분 증가 수열을 구해본다.
  * 시작 인덱스로부터 끝 인덱스까지 각 인덱스를 기준으로 부분 증가수열을 구한다.
  * 부분 증가 수열을 구할 때, 전 인덱스의 부분 수열 갯수를 이용한다.
  * 각 인덱스에서 가장 긴 길이를 가진 수열의 길이를 별도의 리스트에 저장한다.
  * 길이의 최댓값을 출력



## 문제 답안

```python
n = int(input());
arr = list(map(int, input().split()));
arr.insert(0, 0); # 1번 ~n번 리스트
dy = [0] * (n + 1); # 각 인덱스에서의 부분수열 길이
dy[1] = 1; # 첫번째 인덱스의 부분 수열 길이
res = 0; # 답
for i in range(2, n + 1): # 각 인덱스 부분 수열 길이 구하기
    max = 0;
    for j in range(i - 1, 0, -1): # i번째 인덱스 앞 탐색
        if arr[j] < arr[i] and dy[j] > max: 
            max = dy[j];
    dy[i] = max + 1;
    if dy[i] > res:
        res = dy[i];
print(res);
```



# 4. 최대 선 연결하기

## 나의 전략

* 주어진 배열과 오름차순으로 정렬된 배열을 각각 같은 인덱스 번호끼리 연결했을 때, 주어진 배열의 연결된 요소들은 오름차순이다.
* 즉, 첫 인덱스부터 마지막 인덱스까지 각각의 최대 부분 증가 수열을 구하면 된다.



## 문제 해설

* 최대 부분 증가 수열의 최대 길이를 구한다.
* 위 문제의 코드와 동일



## 문제 풀이

```python
n = int(input());
arr = list(map(int, input().split())); # 입력된 배열
arr.insert(0, 0); # 1번 ~n번 리스트
dy = [0] * (n + 1); # 각 인덱스에서의 부분수열 길이
dy[1] = 1; # 첫번째 인덱스의 부분 수열 길이
res = 0; # 답
for i in range(2, n + 1): # 각 인덱스 부분 수열 길이 구하기
    max = 0;
    for j in range(i - 1, 0, -1): # i번째 인덱스 앞 탐색
        if arr[j] < arr[i] and dy[j] > max: 
            max = dy[j];
    dy[i] = max + 1;
    if dy[i] > res:
        res = dy[i];
print(res);
```

* 답안과 동일!



# 5. 가장 높은 탑 쌓기

## 문제 해설

* 벽돌의 밑면의 넓이, 높이, 무게 정보를 구조체로 저장
  * 밑면의 넓이에 대해서 내림차순 정렬
* 무게 조건을 만족하면서 쌓아 올리기
  * 각 벽돌을 기준으로 최대 높이 구하기
  * 전의 벽돌 높이 중에서 최대값 + 자신의 높이
* dy[n]: n번 벽돌을 꼭대기에 올렸을 때, 탑의 최대 높이



## 문제 답안

```python
if __name__ == "__main__":
    n = int(input());
    bricks = []; # 벽돌의 정보를 넣을 리스트
    for i in range(n):
        a, b, c = map(int, input().split()); # 넓이, 높이, 무게
        bricks.append((a, b, c)); # 튜플로 넣기
    bricks.sort(reverse = True); # 내림차순으로 정렬(넓이 기준)
    dy = [0] * n;
    dy[0] = bricks[0][1]; # 0번 벽돌의 높이
    res = bricks[0][1];
    for i in range(1, n): # 1번 벽돌부터 상단의 벽돌로 두기
        max_h = 0;
        for j in range(i - 1, -1, -1):
            if bricks[j][2] > bricks[i][2] and dy[j] > max_h:
                max_h = dy[j]; # i번째 벽돌 전의 최대 높이
        dy[i] = max_h + bricks[i][1];
        res = max(res, dy[i]); # 가장 큰 값
    print(res);
```