# [항해99 1기] [Chapter2-1] 자료구조, 알고리즘 (7) (2021.3.10)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**



# 4949

[문제 링크](https://www.acmicpc.net/problem/4949)

```python
while True:
    string = input()
    if string == ".":
        break
    # 먼저 들어온 괄호가 먼저 나가게 되므로 스택 자료구조형을 사용한다
    stack = []
    # 괄호 탐색
    for x in string:
        # 여는 괄호 발견시 스택에 쌓아두기
        if x == "(" or x == "[":
            stack.append(x)
        # 스택의 마지막 원소의 괄호와 문자열의 괄호가 짝이 맞는지 검사
        elif x == ")":
            if not stack or stack[-1] == "[":
                print("no")
                break
            elif stack[-1] == "(":
                stack.pop()
        elif x == "]":
            if not stack or stack[-1] == "(":
                print("no")
                break
            elif stack[-1] == "[":
                stack.pop()
    # 문자열 탐색이 중단되지 않고 잘 끝나면 yes
    else:
        # 스택에 괄호가 남아있으면 no
        if len(stack) == 0:
            print("yes")
        else:
            print("no")
```



# 1874

[문제 링크](https://www.acmicpc.net/problem/1874)

```python
n = int(input())
# 만들 스택 수열
stack = []
# push할때 사용할 수
push = 0
# 결과를 저장할 리스트
res = []
# 스택이 가능한지 여부
check = True

for i in range(n):
    # 하나하나 입력 받기
    x = int(input())
    # x와 같아질 때 까지 push
    while push < x:
        push += 1
        stack.append(push)
        res.append("+")

    # stack의 마지막과 x가 같은 경우
    if stack[-1] == x:
        stack.pop()
        res.append("-")
    else:
        check = False

if check == False:
    print("NO")
else:
    for x in res:
        print(x)
```



# 1021

[문제 링크](https://www.acmicpc.net/problem/1021)

```python
# 큐 자료구조 사용
from collections import deque

# n : 큐의 크기, m : 뽑아내려고 하는 수의 개수
n, m = map(int, input().split())
# 뽑을 수 입력 받기
find = list(map(int, input().split()))
# 큐 자료구조로 변환
Q = deque(i for i in range(1, n + 1))
# 카운트
count = 0
# 수를 뽑기위해 큐를 1. 왼쪽으로 한 칸 이동 2. 오른쪽으로 한 칸 이동 3. 맨앞의 수 뽑기
# 왼쪽으로 한 칸 이동
def moveLeft():
    # 글로벌 변수
    global count
    count += 1
    num = Q.popleft()
    Q.append(num)


# 오른쪽으로 한 칸 이동
def moveRight():
    # 글로벌 변수
    global count
    count += 1
    num = Q.pop()
    Q.appendleft(num)


# 찾을 수 뽑기
for i in range(m):
    # 큐의 길이
    length = len(Q)
    # 찾을 수가 있는 큐의 인덱스
    qIndex = Q.index(find[i])
    # 찾을 수가 있는 큐의 인덱스가 왼쪽에 더 가까운 경우
    if qIndex < length - qIndex:
        # 맨 앞에 찾을 수가 올 때까지 moveLeft
        while Q[0] != find[i]:
            moveLeft()
        # 뽑아내기
        Q.popleft()
    # 찾을 수가 큐의 인덱스의 오른쪽에 더 가깝거나 중간지점인 경우(상관 없음)
    else:
        # 맨 앞에 수가 올 때까지 moveRight
        while Q[0] != find[i]:
            moveRight()
        # 뽑아내기
        Q.popleft()
print(count)
```



# Comment

한 번에 맞췄다! 기분 좋아라!