# [프로그래머스] 크레인 인형 뽑기 게임 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 크레인 인형뽑기 게임
def solution(board, moves):
    # 집은 인형을 넣을 배열
    pick = []
    # 답
    answer = 0
    # 주어진 moves 배열을 토대로 board를 체크하기
    # x: 집을 인형의 위치
    for x in moves:
        # board의 한 줄 씩 접근
        # borad의 행 길이
        board_row_length = len(board)
        # board의 행 번호
        for i in range(board_row_length):
            # 해당 줄의 집을 위치에 인형이 없는 경우
            if board[i][x - 1] != 0:
                # pick 배열에 인형을 넣기
                pick.append(board[i][x - 1])
                # 해당 시점에서 배열의 길이
                pick_length = len(pick)
                # pick 배열이 길이가 2이상인 배열인 경우 이전의 요소와 비교하기
                if pick_length >= 2:
                    # 같은 인형인 경우 제거한 후 답을 카운트
                    if pick[pick_length - 1] == pick[pick_length - 2]:
                        pick.pop()
                        pick.pop()
                        # 사라진 인형 갯수
                        answer += 2
                # board에서 없애기(0으로 바꾸기)
                board[i][x - 1] = 0
                # 해당  moves 체크 중단
                break
    return answer
```



## Comment

이차원 배열의 요소를 주어진 조건대로 접근하여 빼낸 후, 빼낸 원소들을 별도의 리스트에 담은 뒤 같은 요소가 연달아 나오면 제거하여 카운트하는 문제이다.

내 코드가 좋은 답안 코드와 비슷하게 나와 흡족하다.

# Reference

[프로그래머스](https://programmers.co.kr)

