# [프로그래머스] 로또의 최고 순위와 최저 순위 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 로또의 최고 순위와 최저 순위
def solution(lottos, win_nums):
    answer = []
    # 일치한 수에 다른 순위를 표시하는 딕셔너리
    win_dic = {
        6: 1,
        5: 2,
        4: 3,
        3: 4,
        2: 5,
        1: 6,
        0: 6
    }
    # lottos의 요소를 하나씩 접근하면서  win_nums와 몇 개가 같은 지, 알아볼 수 없는 수(0) 세기
    # 같은 수의 갯수
    same_nums = 0
    # 알아볼 수 없는 수
    zero_count = 0
    for lotto in lottos:
        # lotto가 win_nums 리스트에 존재하는 원소인 경우
        if lotto in win_nums:
            same_nums += 1
        # lotto가 0인 경우
        if lotto == 0:
            zero_count += 1
    # 당첨 가능한 최고 순위: zero_count가 모두 win_nums에 있는 수인 경우 -> same_nums에 zero_count를 더한 수의 순위
    # 당첨 가능한 최저 순위: zero_count가 모두 win_nums에 속하지 않는 경우 -> same_nums에 따른 순위
    answer.append(win_dic[same_nums + zero_count])
    answer.append(win_dic[same_nums])
    return answer
```



## Comment

로또의 순위는 일치한 수에 따라서 정해지므로, 맞은수(key)에 따른 순위(key value)를 표현한 딕셔너리를 선언한다.

그 이후, for문으로 lottos의 요소를 하나씩 접근하며, win_nums에 몇개가 같은지 그리고 0이 얼마나 들어있는지를 센다.

여기서 당첨 가능한 최고 순위를 구하려면 0인 숫자가 win_nums에 모두 속할 때 이므로 0의 갯수만큼을 맞은 수로 더 더한다. 반대로, 당첨 가능한 최저 순위를 구하려면 0인 숫자가 win_nums에 모두 속하지 않을 때이므로 더하지 않는다.

# Reference

[프로그래머스](https://programmers.co.kr)

