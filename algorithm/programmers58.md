# [프로그래머스] 키패드 누르기 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 키패드 누르기
def solution(numbers, hand):
    answer = ''
    # 키패드를 2차원 리스트로 표현했을 때, 각 숫자의 인덱스를 나타내는 딕셔너리
    # key: 숫자, key value: 숫자의 인덱스 [x, y]로 표현
    numbers_dic = {
        1: [0, 0],
        2: [0, 1],
        3: [0, 2],
        4: [1, 0],
        5: [1, 1],
        6: [1, 2],
        7: [2, 0],
        8: [2, 1],
        9: [2, 2],
        '*': [3, 0],
        0: [3, 1],
        '#': [3, 2]
    }
    # left, right의 처음 위치
    left = [3, 0]
    right = [3, 2]
    # 입력받은 numbers를 하나씩 접근
    for number in numbers:
        # number의 인덱스 위치 가져오기
        number_index = numbers_dic[number]
        # 1번 인덱스가 0이면 왼쪽 손가락이 이동
        if number_index[1] == 0:
            # left 위치 최신화
            left = number_index
            # answer에 이동한 손가락 입력
            answer += 'L'
        # 1번 인덱스가 2이면 오른쪽 손가락이 이동
        elif number_index[1] == 2:
            # right 위치 최신화
            right = number_index
            # answer에 이동한 손가락 입력
            answer += 'R'
        # 1번 인덱스가 1이면 두 손가락 중 가까운 손가락이 이동
        else:
            # left와 목표로하는 숫자의 거리
            left_distance = abs(
                number_index[0] - left[0]) + abs(number_index[1] - left[1])
            # right와 목표로하는 숫자의 거리
            right_distacne = abs(
                number_index[0] - right[0]) + abs(number_index[1] - right[1])
            # 둘 중 거리가 작은 손가락이 이동하기
            # left의 거리가 작은 경우
            if left_distance < right_distacne:
                # 손가락 위치 최신화
                left = number_index
                # answer에 이동한 손가락 입력
                answer += 'L'
            # rigth의 거리가 작은 경우
            elif right_distacne < left_distance:
                # 손가락 위치 최신화
                right = number_index
                # answer에 이동한 손가락 입력
                answer += 'R'
            # 두 손가락과 목표로 하는 숫자의 거리가 같은 경우
            elif left_distance == right_distacne:
                # 어느 손잡이인지에 따라 답 입력
                # 왼손잡이
                if hand == 'left':
                    # 손가락 위치 최신화
                    left = number_index
                    # answer에 이동한 손가락 입력
                    answer += "L"
                # 오른손잡이
                else:
                    # 손가락 위치 최신화
                    right = number_index
                    # answer에 이동한 손가락 입력
                    answer += "R"
    return answer
```



## Comment

키패드의 위치를 2차원 리스트에 넣는다고 가정하고 숫자(key), 인덱스(key value)를 별도의 딕셔너리에 선언한다.

왼쪽 손가락과 오른쪽 손가락을 *과 #의 인덱스로 초기화를 하고 for문으로 주어진 numbers를 하나씩 접근한다. number를 선언한 딕셔너리에 넣으면 keyvalue로 해당 인덱스가 나오므로 이것을 이용하여 1번 인덱스가 0이면 왼쪽 손가락의 위치를 해당 인덱스로 최신화 하고 답에 L을 입력한다. 1번 인덱스가 2이면 오른쪽으로 최신화를 하면 된다.

만약 1번 인덱스가 1이면 왼쪽과 오른쪽 손가락 중 가까운 거리의 손가락을 움직여야 한다. 그러므로 목표로 하는 숫자의 인덱스와 각 손가락의 인덱스의 0번과 1번 인덱스를 빼주어 거리를 구한다. 이때 각자 빼기 연산을 할 때 `abs`함수로 절댓값으로 바꾸어야 한다. 그리고 구한 거리가 짧은 쪽의 손가락을 이동 처리한다. 거리가 같은 경우 사용자가 어느 손잡이냐에 따라서 이동처리한다.

# Reference

[프로그래머스](https://programmers.co.kr)

