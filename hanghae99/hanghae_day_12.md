# [항해99 1기] [Chapter2-2] 자료구조, 알고리즘 (10) (2021.3.12)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**



# 10815

[문제 링크](https://www.acmicpc.net/problem/10815)



```python
# 상근이의 숫자 카드의 개수
N = int(input())
# 숫자 카드에 적혀있는 정수
cards = list(map(int, input().split()))
# 정렬
cards.sort()
# 구분할 카드 수
M = int(input())
# 숫자 카드인지 구분할 정수
nums = list(map(int, input().split()))

# 이분탐색
for x in nums:
    # 카드를 소유한 경우
    check = True
    # 시작점
    start = 0
    # 끝점
    end = N - 1
    # 중간점
    mid = (start + end) // 2
    while start <= end:
        if x > cards[mid]:
            start = mid + 1
        elif x < cards[mid]:
            end = mid - 1
        elif x == cards[mid]:
            break
        mid = (start + end) // 2
    else:
        check = False
    # 결과 출력
    if check:
        print(1, end=" ")
    else:
        print(0, end=" ")

```



# 2164

[문제 링크](https://www.acmicpc.net/problem/2164)

```python
# 버리고 -> 옮기고
# 큐 자료형 사용
from collections import deque

# N 입력 받기
N = int(input())
# 카드 생성 1 ~ N
cards = [i for i in range(1, N + 1)]
cards = deque(cards)
# 카드가 한 장 남을 때 까지 버리고 옮기기
while len(cards) > 1:
    cards.popleft()
    # 카드를 버렸을 때 반복문 중단
    if len(cards) == 1:
        break
    # 맨 위의 장을 빼고 뒤로 다시 붙이기
    move = cards.popleft()
    cards.append(move)
# 마지막 남은 카드 출력
print(cards[0])
```



# 2751

[문제 링크](https://www.acmicpc.net/problem/2751)

```python
# N개의 수 입력 받기
N = int(input())
arr = []
for i in range(N):
    arr.append(int(input()))

# 병합 정렬
def merge_sort(arr):
    # 배열의 요소가 하나이면 중단
    if len(arr) <= 1:
        return arr
    # 중간점
    mid = len(arr) // 2
    # 왼쪽 배열
    left_arr = arr[:mid]
    # 오른쪽 배열
    right_arr = arr[mid:]
    # 재귀함수, 가장 작은 단위로 나누기
    return merge(merge_sort(left_arr), merge_sort(right_arr))


def merge(arr1, arr2):
    result = []
    arr1_index = 0
    arr2_index = 0
    # 각 배열의 값들을 하나씩 비교후 더 작은 값 새로운 배열에 추가
    while arr1_index < len(arr1) and arr2_index < len(arr2):
        if arr1[arr1_index] < arr2[arr2_index]:
            result.append(arr1[arr1_index])
            arr1_index += 1
        else:
            result.append(arr2[arr2_index])
            arr2_index += 1
    # 한 배열이 끝나고 난 후 남은 배열의 모든 값을 새로운 배열에 추가
    if arr1_index == len(arr1):
        while arr2_index < len(arr2):
            result.append(arr2[arr2_index])
            arr2_index += 1

    if arr2_index == len(arr2):
        while arr1_index < len(arr1):
            result.append(arr1[arr1_index])
            arr1_index += 1

    return result


sortArr = merge_sort(arr)
for x in sortArr:
    print(x)

```



## Comment

위 3 문제는 오늘 코딩 테스트 문제들. 잘 풀 수 있었다! 마지막 문제는 pypy로 돌릴 것.



# 1316

[문제 링크](https://www.acmicpc.net/problem/1316)

```python
# 단어의 개수 입력 받기
n = int(input())
# 카운트
cnt = 0

# 문자열 하나 하나를 받을 배열
strArr = [""]
# for문으로 반복하며 문자열 입력 받기
for _ in range(n):

    # 문자열 입력 받기
    string = input()
    # 문자열 탐색
    for i in range(len(string)):
        # strArr에 string[i]가 있으면
        if string[i] in strArr:
            if strArr[i] != string[i]:
                strArr = [""]
                break
            elif strArr[i] == string[i]:
                strArr.append(string[i])
        else:
            strArr.append(string[i])
    else:
        cnt += 1
        strArr = [""]
print(cnt)
```



## Comment

디버깅을하며 차근차근 풀어서 올바른 답을 낼 수 있었다!



# 2839

[문제 링크](https://www.acmicpc.net/problem/2839)

```python
# 3킬로그램 봉지, 5킬로그램 봉지
# 설탕 킬로그램 수
n = int(input())
# 카운트
cnt = 0
# 무한루프
while True:
    # n이 음수가 되어버리면 -1 출력 후 중단
    if n < 0:
        print(-1)
        break
    # n이 5로 나누어 떨어지면 그 몫이 최솟값이므로 바로 출력하기
    if n % 5 == 0:
        cnt += n // 5
        print(cnt)
        break
    # 아니라면 -3을 해주면서 봉지수를 카운트하기
    else:
        n -= 3
        cnt += 1
```

## Comment

가장 좋은 경우가 5로 나누어떨어지는 경우이다. 나누어 떨어지지 않는다면 3을 하나씩 빼주면서 다시 5로 나누어 떨어지는 지 검사해보는 것으로 답을 구할 수 있었다.



# 1011

[문제 링크](https://www.acmicpc.net/problem/1011)

```python
# math 모듈 가져오기
import math

# 테스트 케이스 개수 입력 받기
t = int(input())
# 테스트 케이스 개수만큼 반복하여 x, y 좌표의 최소 공간 장치 작동 횟수 구하기
for _ in range(t):
    x, y = map(int, input().split())
    # 거리
    d = y - x
    # 3 이하는 그대로 출력
    if d <= 3:
        print(d)
    else:
        # d의 제곱근 구하고 정수화
        sqD = int(math.sqrt(d))
        # d와 제곱근의 관계에 따라서 작동 횟수가 달라진다.
        # d가 정수의 제곱근을 가지는 경우
        if d == (sqD ** 2):
            print(2 * sqD - 1)
        # d가 sqD의 제곱 + sqD 보다 작은 경우
        elif sqD ** 2 < d <= sqD ** 2 + sqD:
            print(2 * sqD)
        # d가 sqD의 제곱 + sqD보다 큰 경우
        else:
            print(2 * sqD + 1)
```



#  4948

[문제 링크](https://www.acmicpc.net/problem/4948)

```python
# 베르트랑 공준
# 임의의 자연수 n에 대해서 n보다 크고 2n보다 작거나 같은 소수를 세기
# 에라토스테네스의 체로 소수 배열을 만들고 주어진 수의 범위에서의 소수 세기

# 입력 받기
while True:
    n = int(input())
    # 0 입력 시 중단
    if n == 0:
        break
    # 베르트랑 공준 구하기
    # 1인 경우 바로 출력
    elif n == 1:
        print(n)
    else:
        # 소수 배열 만들기, 0으로 초기화
        ch = [0] * ((n * 2) + 1)
        # 카운트
        cnt = 0
        # n부터 2n 범위 내의 소수를 구하는 에라토스테네스의 채
        # 2부터 체크해 나가기
        for i in range(2, (n * 2) + 1):
            # ch[i]가 0일 경우(2부터) 소수 체크
            if ch[i] == 0:
                # 주어진 수 n 보다 클 경우 소수로 체크
                if i > n:
                    cnt += 1
                # 해당 소수의 배수를 소수가 아닌 수로 체크
                # 가장 작은 배수 (2)부터 시작, 자기 자신을 체크하지 않기 위해서
                #  step i로 주어서 증가(배수)
                for j in range(i * 2, (n * 2) + 1, i):
                    # 배수인 경우 체크
                    ch[j] = 1
        print(cnt)
```



# 1436

[문제 링크](https://www.acmicpc.net/problem/1436)

```python
# n번째 영화를 출력
n = int(input())
# 카운트
cnt = 0
# 시작수
num = 666
# 숫자를 받을 리스트
arrNum = []
# 무한루프 반복문으로 n번째 영화를 출력
while True:
    # 숫자 탐색을 위해 문자열로 바꾸기
    strNum = str(num)
    # 문자열로 바꾼 숫자에 "666"이 있으면 카운트
    if "666" in strNum:
        cnt += 1
        # 주어진 카운트 수를 만족하면 num 프린트 후 break
        if cnt == n:
            print(num)
            break
    # 찾는 수가 나오지 않았으므로 1 더하기
    num += 1
```



## Comment

브루트 포스 알고리즘 문제이다. 처음에 보고 어? 너무 쉽잖아 하고 문자열로 답을 만들려고 했는데 잘못 이해한 것이었다. 제대로 이해하고 난 후 구현하는 것은 어렵지 않았다. 문자열 또한 in을 사용할 수 있는 것을 잘 기억하자.