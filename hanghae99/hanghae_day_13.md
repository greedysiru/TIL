# [항해99 1기] [Chapter2-2] 자료구조, 알고리즘 (11) (2021.3.13)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**



# 9184

 [문제 링크](https://www.acmicpc.net/problem/9184)

```python
def w(a, b, c):
    # 메모에 전달받은 인자값들이 키로 있으면 그 값을 리턴
    if (a, b, c) in memo.keys():
        # memo 딕셔너리의 (a, b, c) 값 리턴
        return memo[(a, b, c)]

    # 문제에서 제시된 조건을 이용하여 메모이제이션
    if a <= 0 or b <= 0 or c <= 0:
        # 메모이제이션
        memo[(0, 0, 0)] = 1
        return 1

    elif a > 20 or b > 20 or c > 20:
        # 메모이제이션
        memo[(20, 20, 20)] = w(20, 20, 20)
        return memo[(20, 20, 20)]

    elif a < b < c:
        # 메모이제이션
        memo[(a, b, c)] = w(a, b, c - 1) + w(a, b - 1, c - 1) - w(a, b - 1, c)
        return memo[(a, b, c)]

    else:
        # 메모이제이션
        memo[(a, b, c)] = w(a - 1, b, c) + w(a - 1, b - 1, c) + \
            w(a - 1, b, c - 1) - w(a - 1, b - 1, c - 1)
        return memo[(a, b, c)]

# 메모이제이션
memo = {}

# 입력받기
# -1 -1 -1이면 입력 받기 중단
while True:
    a, b, c = map(int, input().split())
    if a == -1 and b == -1 and c == -1:
        break
    print("w(", a, ", ", b, ", ", c, ")", " = ", w(a, b, c), sep="")
```



## Comment

처음 문제를 봤을 때 무작정 주어진 점화식을 코드로 작성했는데 작은 수에서는 잘 나왔지만 조금만 커져도 재귀함수 호출로 인해 시간초과가 나왔다. 하지만, 동적 계획법의 핵심 요소인 메모이제이션을 활용하니 놀랍게도 바로 해결해낼 수 있었다. 디버깅 모드로 하나하나 어떻게 실행되었는지 봤는데 큰 숫자가 입력되어도 재귀 함수고 호출되며 상수값이 리턴될 때마다 메모이제이션이 되는 것을 볼 수 있었다. 메모이제이션의 강력함을 깨달을 수 있는 좋은 문제였던 것 같다.



# 9461

[문제 링크](https://www.acmicpc.net/problem/9461)

```python
# 메모이제이션
memo = {
    1: 1,
    2: 1,
    3: 1,
    4: 2,
    5: 2,
    6: 3,
    7: 4,
    8: 5,
    9: 7,
    10: 9,
    11: 12
}
# 파도반 수열 구하기
def P(n):
    # memo 딕셔너리에 있는 키면 바로 그 값을 리턴
    if n in memo:
        return memo[n]
    # memo가 없는 경우
    else:
        # 메모이제이션을 재귀함수로 넣어준 후 그 키값을 리턴
        memo[n] = P(n - 1) + P(n - 5)
        return memo[n]

# 테스트케이스
T = int(input())
for _ in range(T):
    n = int(input())
    print(P(n))
```



## Comment

동적 계획법에 따라 작은 경우들을 메모이제이션을 하였고 이 메모이제이션을 활용해서 값을 구할 수 있도록 하였다. 파도반 수열의 점화식은 직접 그려보면서 어떤 값들을 더해야 나오는지 분석하니 금방 구할 수 있었다.



# 1149

[문제 링크](https://www.acmicpc.net/problem/1149)

```python
# 집의 수 입력받기
N = int(input())
# 집을 칠하는 비용 입력 받기
home = []
for _ in range(N):
    home.append(list(map(int, input().split())))
# minCost는 각 인덱스(시점)에서의 비용을 기록하는 리스트
# 0번 인덱스 : 빨간색, 1번 인덱스: 초록색, 2번 인덱스: 파란색
# 처음 시점(0번 인덱스)에서의 최소 비용은 주어진 값 그대로이므로 초기화값으로 넣어준다.
minCost = [home[0]]
# 입력받은 비용 정보를 토대로 비용 최솟값 구하기
for i in range(1, N):
    # i번째 집이 빨간색, 초록색, 파란색일 때 각각의 경우의 최솟값을 구한다.
    home_red = home[i][0] + min(minCost[i - 1][1], minCost[i - 1][2])
    home_green = home[i][1] + min(minCost[i - 1][0], minCost[i - 1][2])
    home_blue = home[i][2] + min(minCost[i - 1][1], minCost[i - 1][0])
    # 각각의 경우를 append 한다.
    minCost.append([home_red, home_green, home_blue])
# 최솟값을 출력한다.
print(min(minCost[N - 1]))
```



## Comment

문제를 잘못 파악해서 엉뚱한 곳을 짚었던 문제. 각 시점에서의 최솟값을 경우별로 정리하여 풀 수 있다. 빨간색으로 칠할 때, 전의 집이 파란색이나 초록색이어야 하므로 그 둘 중 최소비용을 가져와서 빨간색으로 칠한 비용과 합해준다. 그리고 색깔별로 분류한 각 인덱스(답을 기록하는 리스트)에 기록하고(메모이제이션) 매번 전의 인덱스를 참조하여 더해나간다.



# 1932

[문제 링크](https://www.acmicpc.net/problem/1932)

```python
# 삼각형의 크기
n = int(input())


# 삼각형의 정보를 받을 리스트
tri = []
for _ in range(n):
    tri.append(list(map(int, input().split())))

for i in range(1, n):
    for j in range(len(tri[i])):
        if j == 0:
            tri[i][j] = tri[i - 1][j] + tri[i][j]
        elif j == i:
            tri[i][j] = tri[i - 1][j - 1] + tri[i][j]
        else:
            tri[i][j] = max(tri[i - 1][j - 1],
                            tri[i - 1][j]) + tri[i][j]
print(max(tri[n - 1]))
```

## Comment

손코딩의 중요성을 깨달았다. 차근차근히 손으로 써보면서 문제를 풀자.

# 11047

[문제 링크](https://www.acmicpc.net/problem/11047)

```python
# N가지의 동전, K원
N, K = map(int, input().split())
# 동전 가치 입력 받기
coin = []
for _ in range(N):
    coin.append(int(input()))

# 동전을 내림차순으로 정렬
coin.sort(reverse=True)
# 카운트
cnt = [0] * N
for i in range(len(coin)):
    # 접근한 동전의 가치가 K보다 큰 경우 넘어간다.
    if coin[i] > K:
        continue
    # K를 나눈 나머지가 0이면 cnt에 그 몫을 넣고 총합을 출력
    elif K % coin[i] == 0:
        cnt[i] = K // coin[i]
        print(sum(cnt))
        break
    else:
        # 현재 금액으로 나눈 몫을 넣고 K에 현재 나눈 나머지를 넣는다.
        cnt[i] = K // coin[i]
        K = K % coin[i]

```

## Comment

그리디알고리즘의 핵심을 기억하고 현재할 수 있는 가장 최상의 답을 넣어간다는 생각으로 풀어서 빠르게 해결할 수 있었다.



# 11399

[문제 링크](https://www.acmicpc.net/problem/11399)

```python
# 사람의 수
N = int(input())
# 돈을 인출하는데 걸리는 시간
T = list(map(int, input().split()))
T.sort()
# 누적되는 시간
S = 0
for i in range(N):
    for j in range(i + 1):
        S += T[j]
print(S)
```

## Comment

첫번째 사람이 가장 빠르게 할 수록 총 합이 낮아지므로 받은 시간 값을 오름차순 정렬후 for문을 사용하여 누적합을 더하도록 하였다.



# 1037

[문제 링크](https://www.acmicpc.net/problem/1037)

```python
# N의 진짜 약수 개수
ea = int(input())
# N의 진짜 약수
divisors = list(map(int, input().split()))
# 진짜 약수에서 가장 작은수 * 가장 큰수 = N
print(min(divisors) * max(divisors))
```



# 2609

[문제 링크](https://www.acmicpc.net/problem/2609)

```python
# 두 수의 최대공약수, 최소공배수를 구하기
A, B = map(int, input().split())
# 유클리드 호제법을 사용하여 최대공약수 구하기
a = A
b = B
while b != 0:
    r = a % b
    a = b
    b = r
# 최대 공약수
G = a
# 최소공배수
L = int((A / G) * (B / G) * G)
print(G)
print(L)
```



# 1934

[문제 링크](https://www.acmicpc.net/problem/1934)

```python
# 유클리드 호제법으로 최대공약수 구하는 함수
def euclid(a, b):
    while b != 0:
        r = a % b
        a = b
        b = r
    G = a
    return G

# 최소공배수 구하는 함수

def LCM(a, b):
    G = euclid(a, b)
    L = int((a / G) * (b / G) * G)
    return L

T = int(input())
for i in range(T):
    a, b = map(int, input().split())
    print(LCM(a, b))
```



# 11050

[문제 링크](https://www.acmicpc.net/problem/11050)

```python
N, K = map(int, input().split())

# 팩토리얼 함수
def factorial(n):
    result = 1
    # 1부터 n까지의 수를 차례대로 곱하기
    for i in range(1, n + 1):
        result *= i
    return result

# 이항계수
if K < 0:
    print(0)
elif K > N:
    print(0)
elif 0 <= K and K <= N:
    # N, K의 팩토리얼을 각각 구한 후 이항계수 계산
    facN = factorial(N)
    facK = factorial(K)
    facNK = factorial(N - K)
    print(int(facN / (facK * (facNK))))
```



## Comment

이항정리의 정의를 찾아서 식으로 적용할 수 있도록 했다.



# 1010

[문제 링크](https://www.acmicpc.net/problem/1010)

```python
# 다리가 겹쳐지는 것이 안된다 -> 순서가 포함된다 -> 조합
# 테스트 케이스
T = int(input())
# 팩토리얼 함수

def factorial(n):
    result = 1
    for i in range(1, n + 1):
        result *= i
    return result

# 강의 서쪽과 동족에 있는 사이트의 개수를 받기
for _ in range(T):
    N, M = map(int, input().split())
    print(int(factorial(M) / (factorial(N) * factorial(M - N))))
```



# 10828

[문제 링크](https://www.acmicpc.net/problem/10828)

```python
import sys

# 스택 구현


class stack:
    def __init__(self):
        # 길이 0
        self.len = 0
        # 리스트 자료형을 기본으로 생성
        self.list = []

    # push 함수
    def push(self, val):
        # 리스트에 val 추가하기
        self.list.append(val)
        # 원소가 늘어났으므로 +1
        self.len += 1

    # size 함수
    def size(self):
        # stack의 len 속성을 리턴
        return self.len

    # pop 함수
    # 가장 위에 있는 정수 빼기
    def pop(self):
        #  stack이 없는 경우
        if self.size() == 0:
            return -1
        # 가장 위에 있는 정수 빼기
        result = self.list[self.len - 1]
        # 지우기
        del self.list[self.len - 1]
        # 원소가 빠졌으므로 -1
        self.len -= 1
        # 지운 값 리턴
        return result

    # empty 함수
    def empty(self):
        # 비어있을 때 참
        if self.len == 0:
            return 1
        else:
            return 0

    # top 함수
    def top(self):
        if self.size() != 0:
            return self.list[-1]
        else:
            return -1
          
# 주어지는 명령의 수
N = int(input())
# 스택 생성
stack = stack()
for _ in range(N):
    # 시간초과 방지
    # 한줄씩 받되 오른쪽의 공백을 삭제하고 띄어쓰기를 기준으로 나눈다.
    command = sys.stdin.readline().rstrip().split()
    # 인덱싱으로 command에 입력된 명령어를 각각 접근 가능
    if command[0] == "push":
        stack.push(command[1])
    elif command[0] == "pop":
        print(stack.pop())
    elif command[0] == "size":
        print(stack.size())
    elif command[0] == "empty":
        print(stack.empty())
    elif command[0] == "top":
        print(stack.top())
```



# 10773

[문제 링크](https://www.acmicpc.net/problem/10773)

```python
# K의 개의 줄
K = int(input())
# 스택
stack = []

# 입력 받기
for _ in range(K):
    num = input()
    # 0일 경우 가장 최근에 들어온 원소 제거
    if num == "0":
        stack.pop()
    else:
        stack.append(int(num))
print(sum(stack))
```



# 9012

[문제 링크](https://www.acmicpc.net/problem/9012)

```python
# 테스트 케이스
T = int(input())
# 괄호 입력 받기
for _ in range(T):
    bracket = list(input())
    # 입력 받은 괄호 확인하기
    cnt = 0
    for i in range(len(bracket)):
        # 여는 괄호이면 + 1
        if bracket[i] == "(":
            cnt += 1
        # 닫는 괄호이면 - 1
        elif bracket[i] == ")":
            cnt -= 1
        # 음수가 되면 NO 출력후 중단
        if cnt < 0:
            print('NO')
            break
    # 탐색 후 양수이면 NO
    if cnt > 0:
        print('NO')
    elif cnt == 0:
        print('YES')
```



# 18258

[문제 링크](https://www.acmicpc.net/problem/18258)

 ```python
import sys
from collections import deque
# 주어지는 명령의 수
N = int(input())
# 큐 생성
Q = deque([])
for _ in range(N):
    # 시간초과 방지
    # 한줄씩 받되 오른쪽의 공백을 삭제하고 띄어쓰기를 기준으로 나눈다.
    command = sys.stdin.readline().rstrip().split()
    # 인덱싱으로 command에 입력된 명령어를 각각 접근 가능
    if command[0] == "push":
        Q.append(command[1])
    elif command[0] == "pop":
        if len(Q) == 0:
            print(-1)
        else:
            print(Q.popleft())
    elif command[0] == "size":
        print(len(Q))
    elif command[0] == "empty":
        if len(Q) == 0:
            print(1)
        else:
            print(0)
    elif command[0] == "front":
        if len(Q) == 0:
            print(-1)
        else:
            print(Q[0])
    elif command[0] == "back":
        if len(Q) == 0:
            print(-1)
        else:
            print(Q[-1])
 ```

