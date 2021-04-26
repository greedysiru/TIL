




# [프로그래머스] 주식가격 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 주식가격
def solution(prices):
    # 떨어지지 않은 시간을 넣을 리스트
    answer = []
    # prices의 길이
    prices_len = len(prices)

    # prices를 접근
    for i in range(prices_len):
        # 떨어지지 않은 시간
        time = 0
        for j in range(i + 1, prices_len):
            time += 1
            # 가격이 내려간 경우
            if prices[i] > prices[j]:
                break
        # time를 answer에 넣기
        answer.append(time)
    return answer
```



## Comment

큐 문제라서 deque를 사용했었는데 시간초과 오류가 떴다. 그래서 이중for문으로 다시 풀어보니 효율성에서 통과! 

# Reference

[프로그래머스](https://programmers.co.kr)