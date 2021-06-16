# [프로그래머스] 조이스틱 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 조이스틱
def solution(name):
    answer = 0
    # name의 길이
    name_len = len(name)
    # name을 리스트화 한 후 아스키 코드로 변환
    name_list = list(name)
    # 기본 문자인 A와 목표로하는 문자의 아스키 코드 차이를 구하여 리스트에 넣기
    deference_list = []
    for i in range(name_len):
        deference = ord(name_list[i]) - 65
        if deference > 12:
            deference = 26 - deference
        deference_list.append(deference)
    # deference_list를 0번 index 부터 접근
    idx = 0
    while True:
        # deference_list의 각 요소는 조이스틱을 움직여야 하는 수이므로 답에 더한다.
        answer += deference_list[idx]
        # 답을 더했으므로 0을 대입
        deference_list[idx] = 0
        # deference_list의 총합이 0이면 모든 요소를 접근하였으므로 중단
        if sum(deference_list) == 0:
            break
        # 오른쪽으로 갔을 때의 이동수와 왼쪽으로 갔을 때의 이동수
        right_move = 1
        left_move = 1
        # 각 경우에서 0이 아닌 요소가 나올 때 까지 이동
        # 오른쪽
        while deference_list[idx + right_move] == 0:
            right_move += 1
        # 왼쪽
        while deference_list[idx - left_move] == 0:
            left_move += 1
        # 더 적은 이동수를 인덱스에 누적, 답에 누적한다.(최소가 되는 이동수)
        if right_move <= left_move:
            idx += right_move
            answer += right_move
        else:
            idx -= left_move
            answer += left_move
    return answer
```



## Comment

그리드 알고리즘을 사용하는 문제.

각 문자는 고유의 아스키 코드(정수)가 있으므로 , 문자 A와 목표로 하는 문자의 아스키 코드 차이를 구한다. 이 때, 차이가 12를 초과하면 아래 조이스틱을 사용하는 것이 더 최소값이므로 26에서 차이를 뺀다. (총 26개의 문자이므로)

차이가 담긴 리스트의 요소를 반복문으로 하나씩 접근한다. 이때 리스트에 담긴 요소는 answer에 누적하고 해당 요소에는 0을 대입한다. 그리고 왼쪽 이동수, 오른쪽 이동수를 1로 초기화 한 뒤,**그리디 알고리즘**으로 왼쪽으로 갔을 때와 오른쪽으로 갔을 때의 수를 인덱스에 더하여 0이 아닌 요소가 나오는 최소 이동수를 구한다. 이 최소 이동수는 접근할 인덱스와 answer에 누적한다. 그러면 반복문으로 인해서 다시 리스트에 담긴 요소는 answer에 누적될 것이고 0이 대입될 것이다. 이 때, 매번 리스트의 총합을 체크하여 0이 되면 반복문을 완전히 중단하면 된다. 0이 아니라면, 다시 최소 이동수 그리디 알고리즘을 실행한다.

# Reference

[프로그래머스](https://programmers.co.kr)

