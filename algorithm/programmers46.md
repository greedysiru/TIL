# [프로그래머스] 야근 지수 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 야근 지수
import heapq

def solution(n, works):
    answer = 0
    h = []
    # 입력받은 works를 최대힙으로 변환 (부호 반대로 입력)
    for work in works:
        heapq.heappush(h, -work)
    # n이 0이 될 때까지 h의 모든 요소가 최소가 되도록 빼기
    while n != 0:
        n -= 1
        # 현재 시점에서 가장 최대인 요소
        max_work = -heapq.heappop(h)
        # 최대인 요소가 0이면 반복문 중단
        if max_work == 0:
            break
        # 1을 빼고 h에 넣기
        max_work -= 1
        # 최대힙이므로 부호를 반대로 넣기
        heapq.heappush(h, -max_work)
    # 야근 지수 구하기
    for left in h:
        left **= 2
        answer += left
    return answer
```



## Comment

최대힙을 사용하여 풀었다. 주어진 works 리스트를 최대힙으로 변환하여야 한다. 파이썬의 heapq는 기본이 최소힙이다. 그러므로 최대힙을 적용하기 위해서 heappush를 사용하여 요소를 넣을 때 음수로 바꾸어야 하고 heappop을 사용해서 힙의 최대 요소를 뺄 때도 음수를 붙여서 빼야 한다.

야근 지수는 주어진 works의 각 요소를 총 n 만큼 뺐을 때의 각 요소 제곱의 합이다. works의 각 요소를 최소화하기 위해서 반복문으로 매번 최대 요소를 가져온 뒤 1을 빼고 다시 힙에 넣는다. 이때, n이 0이 되거나 빼낸 최대 요소가 0이면 반복문을 중단한다. 최대 요소가 0이면 나머지 요소도 0이므로 더 진행하게 된다면, 음수로 되기 때문이다.

# Reference

[프로그래머스](https://programmers.co.kr)

