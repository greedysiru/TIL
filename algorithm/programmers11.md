
# [프로그래머스] 예산 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 예산
def solution(d, budget):
    # 몇개에 부서에 예산을 줄 수 있는지 세는 변수
    answer = 0
    # 가장 작은 수부터 적용해야 최대 부서 수를 구할 수 있으므로 내림차순으로 정렬(pop을 사용)
    d.sort(reverse=True)
    # while문으로 d가 빌 때까지
    while d:
        # 현재 시점에서 가장 예산이 적은 부서
        d_min = d.pop()
        # 남은 예산이 부서 예산보다 작으면 중단
        if d_min > budget:
            break
        # 크거나 작으면 실행
        elif d_min <= budget:
            budget -= d_min
            # 카운트하기
            answer += 1
    return answer
```



## Comment

가장 작은 예산 범위를 가진 부서부터 총 예산을 차감해가야 지원할 수 있는 부서의 수가 최대로 된다는 것을 염두하고 코드를 작성하였다.

# Reference

[프로그래머스](https://programmers.co.kr)

