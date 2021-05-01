


# [프로그래머스] 카펫 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 카펫
def solution(brown, yellow):
    # 답을 담을 배열
    answer = []
    # 노란색 격자의 가로 길이
    yellow_width = 0
    # 노란색 격자의 세로 길이
    yellow_height = 0
    # 갈색 격자의 수를 구하는 공식
    # (yellow_wdith * 2) + (yellow_height * 2) + 4
    # 위 식을 이용하여 주어진 갈색 격자의 수가 나오는 노란색 격자의 가로, 세로의 조건을 찾는다
    while True:
        # 노란색 격자의 높이를 1씩 더하기
        yellow_height += 1
        # 노란색 격자의 가로길이 구하기
        yellow_width = yellow / yellow_height
        # 위 조건에서의 갈색 격자의 수
        brown_amount = (yellow_width * 2) + (yellow_height * 2) + 4
        # brown_amount가 brown과 같으면 해를 찾았으므로 중단
        if brown_amount == brown:
            # 총 가로길이, 세로길이는 노란 격자의 가로, 세로길이의 +2 이다.
            answer.append(yellow_width + 2)
            answer.append(yellow_height + 2)
            break
    return answer
```



## Comment

카펫의 가로, 세로길이를 구하기 위해서 노란색 격자의 세로 길이에 따른 갈색 격자의 갯수를 구해내는 식을 구해내었다. 그리고 이것을 토대로 주어진 갈색 갯수를 나오게 하는 노란색 격자의 가로, 세로길이를 구한 뒤 2씩 더하여 답을 구해낼 수 있었다.

# Reference

[프로그래머스](https://programmers.co.kr)