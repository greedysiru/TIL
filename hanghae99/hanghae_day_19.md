# [항해99 1기] [Chapter2-2] 자료구조, 알고리즘 (17) (2021.3.19)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제로 알고리즘 테스트**



# 1920

[문제 링크](https://www.acmicpc.net/problem/1920)

```python
import sys
# 자연수 N 입력 받기
N = int(input())
# 정수 N개 입력 받기
arr1 = list(map(int, sys.stdin.readline().split()))
# 자연수 M입력 받기
M = int(input())
# 정수 M개 입력 받기
arr2 = list(map(int, sys.stdin.readline().split()))
# arr1 오름차순 정렬
arr1.sort()
# arr2의 정수가 arr1에 존재하는지 출력하기
# 존재할 경우 1, 존재하지 않을 경우 0 출력
# 이분 탐색
for i in range(M):
    # 시작점
    start = 0
    # 끝점
    end = len(arr1) - 1
    # 중간점
    mid = (start + end) // 2
    #  시작점이 끝점보다 작거나 같을 때 실행
    while start <= end:
        # 값을 찾았을 때(존재할 때)
        if arr2[i] == arr1[mid]:
            # 출력 후 break
            print(1)
            break
        # 찾는 값이 중간값보다 클 때
        elif arr2[i] > arr1[mid]:
            # 시작점을 올리기
            start = mid + 1
        # 찾는 값이 중간값보다 작을 때
        elif arr2[i] < arr1[mid]:
            # 끝점을 내리기
            end = mid - 1
        # 중간점을 최신화
        mid = (start + end) // 2
    # 찾을 수 없었을 때(존재하지 않을 때)
    else:
        print(0)
```



## Comment 

탐색은 가능하면 이분탐색으로 해야 시간초과가 뜨지 않는다.



# 15649

[문제 링크](https://www.acmicpc.net/problem/15649)

```python
def makeS(L):
    # L은 가져온 수열의 숫자
    # M만큼 만들게되면 수열 출력하기
    if L == M:
        for i in range(L):
            # 옆으로 출력
            print(S[i], end=" ")
        # 줄바꾸기
        print()
    else:
        # 1부터 N까지의 수열 넣기
        for j in range(1, N + 1):
            # 아직 넣지 않은 숫자이면 실행
            if check[j] == 0:
                # 수열에 숫자 넣기
                S[L] = j
                # 체크하기
                check[j] = 1
                # 숫자 하나 더 고르기
                makeS(L + 1)
                # 돌아온 시점(출력후)에서 체크리스트 초기화
                check[j] = 0


# 자연수 N과 M
N, M = map(int, input().split())
# 만들 수열을 담을 리스트
S = [0] * M
# 인덱스가 수열의 숫자를 표시하는 체크리스트
check = [0] * (N + 1)
# 수열을 만드는 깊이 우선 탐색 함수 호출
makeS(0)
```



# 1904

[문제 링크](https://www.acmicpc.net/problem/1904)

## 오류가 발생한 코드

```python
# 자연수 N
N = int(input())
# 메모이제이션
memo = {
    1: 1,
    2: 2
}


# 주어진 조건에서 길이가 N인 2진 수열의 개수를 15746으로 나눈 나머지 구하기
# 주어진 길이에서의 2진 수열의 개수를 구하는 함수 정의
# 점화식: make_binary(N) = make_binary(N - 2) + make_binary(N - 1)
def make_binary(N):
    # 1과 2일때는 메모이제이션된 값 리턴
    if N == 1:
        return memo[1]
    elif N == 2:
        return memo[2]
    # N이 memo에 key로 존재하면 해당하는 값 리턴
    elif N in memo.keys():
        return memo[N]
    # 존재하지 않으면 점화식으로 함수 호출, 메모이제이션하기
    else:
        # N길이를 갖는 2진 수열은 N-2 때와 N-1 때의 수열의 길이를 합한 것과 같다.
        memo[N] = (make_binary(N - 1) + make_binary(N - 2)) % 15746
        # 해당하는 메모이제이션 리턴
        return memo[N]


# N의 길이를 가지는 2진 수열의 개수를 15746으로 나눈 나머지 출력
print(make_binary(N))
```



## 정답

```python
# 자연수 N
N = int(input())
# 메모이제이션
memo = {
    1: 1,
    2: 2
}

#  주어진 수까지 점화식을 이용하여 메모이제이션하기
# 점화식: memo[i] = memo[i - 1] + memo[i - 2]
# 길이가 N일 때의 만들 수 있는 모든 2진 수열의 개수는 N-1, N-2 일때 만들 수 있는 2진 수열의 합과 같다.
# 3 부터 주어진 수 N까지 메모이제이션
for i in range(3, N + 1):
    # 만들어진 가짓수를 문제에서 주어진 15746을 나눈 나머지로 기록
    memo[i] = (memo[i - 1] + memo[i - 2]) % 15746
# 답 출력
print(memo[N])
```



## Comment

1부터 7까지의 경우를 직접 써보면서 점화식을 찾았고 메모이제이션을 할 수 있도록 하였다. 여기서, 숫자가 커지면 메모이제이션을 하더라도 재귀함수 호출로는 Recursion Error 가 발생하므로 주의.