# [항해99 1기] [Chapter2-1] 자료구조, 알고리즘 (5) (2021.3.9)

**[Baekjoon Online Judge](https://www.acmicpc.net/)**

**백준 온라인 저지 사이트의 문제 풀이**



# 11729

[문제 링크](https://www.acmicpc.net/problem/11729)

```python
n = int(input())
# 옮긴 횟수
count = 0
# 하노이의 탑 원반 옮기기 함수
def moveDisk(d, s, m, e):  # d: 원반 갯수, s: 출발 장대, m: 중간 장대, e: 마지막 장대
    # 원반을 다 옮기면 재귀함수 호출 종료
    if d == 0:
        return
    # 원반을 중간 장대에 이동
    moveDisk(d - 1, s, e, m)
    # 가장 큰 원반을 마지막 장대로 이동
    print(s, e)

    # 중간 장대의 원반을 마지막 장대로 옮기기
    moveDisk(d - 1, m, s, e)


for i in range(n):
    count = count * 2 + 1
print(count)
moveDisk(n, 1, 2, 3)
```



## Comment

재귀함수는 이해했다고 생각했는데 하노이의 탑을 만난 순간 탑 무너지듯 무너져 버렸다.

아래는 재귀함수를 정리하고 하노이의 탑 해설을 들을 좋은 강의

[유튜브 링크](https://www.youtube.com/watch?v=aPYE0anPZqI)



# 11651

[문제 링크](https://www.acmicpc.net/problem/11651)

```python
n = int(input())
# 점들을 받을 리스트 생성
points = []
for _ in range(n):
    x, y = map(int, input().split())
    points.append([x, y])
# 람다식을 사용하여 y를 기준으로 정렬 후 x를 기준으로 정렬
points.sort(key=lambda x: (x[1], x[0]))
# 정렬한 요소를 하나씩 접근
for a in points:
    # 인덱스 0,1 을 나란히 출력후 줄바꿈
    for i in range(2):
        print(a[i], end=" ")
    print("")
```



# 2805

[문제 링크](https://www.acmicpc.net/problem/2805)

```python
# 자르는 높이를 이진 탐색하기
# n: 나무의 수, m: 가지고 갈 나무의 길이
n, m = map(int, input().split())
# 나무의 높이
trees = list(map(int, input().split()))
# 자르는 높이의 시작점
start = 1
# 결과값
res = 0
# 자르는 높이의 끝점
end = max(trees)

def sumCut(mid):
    # 잘린 나무의 높이
    cut = 0
    for tree in trees:
        if tree > mid:
            cut += tree - mid
    return cut

while start <= end:

    # 자르는 높이의 중간점(절단기의 현재 높이)
    mid = (start + end) // 2
    cut = sumCut(mid)
    # 더 잘렸거나 맞게 잘랐을 때
    if cut >= m:
        start = mid + 1
        # 최댓값 구하기
        if res < mid:
            res = mid
    # 덜 잘렸을 때
    elif cut < m:
        end = mid - 1
print(res)
```



# Comment

이전에 다른 동기님이 파이썬 시간초과 문제로 튜터님께 여쭤본 적 이 있는데, 나무를 자른 높이를 구하기 위해 for문을 돌린 부분에서 [python function caching](https://book.pythontips.com/en/latest/function_caching.html)이라는 것 때문에 함수화를 해야한다고 하셨다. 조금 잘못된 기준이니 신경쓰지는 말라고 하셨지만 혹시나하니 코멘트 남겨놓는다.

