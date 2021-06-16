# [프로그래머스] 메뉴 리뉴얼 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 메뉴 리뉴얼
from itertools import combinations
def solution(orders, course):
    answer = []
    # 주어진 coruse의 요소를 하나씩 접근(menu_ea: 메뉴의 갯수)
    for menu_ea in course:
        # 조합을 담을 빈 딕셔너리 선언
        combinations_dic = {}
        # 주어진 orders의 요소를 하나씩 접근 (order: 각 손님이 주문한 단품메뉴들)
        for order in orders:
            # 각 손님이 주문한 단품 메뉴들을 기반으로, 메뉴 수만큼의 조합 만들어서 리스트로 넣기
            # 오름차순 정렬을 하여, 단품 메뉴 순서를 통일화
            order_combinations = list(combinations(sorted(order), menu_ea))
            # 만들어진 조합을 하나씩 접근
            for order_combination in order_combinations:
                # 튜플 형태의 조합을 문자열화
                order_combination = ''.join(order_combination)
                # 딕셔너리에 현재 조합이 없으면 key를 생성하고 1을 입력
                if order_combination not in combinations_dic:
                    combinations_dic[order_combination] = 1
                # 딕셔너리에 현재 조합이 key로 있는 경우, 1을 누적
                else:
                    combinations_dic[order_combination] += 1
        # 만들어진 딕셔너리의 key, value 접근
        for key, value in combinations_dic.items():
            # 현재 딕셔너리의 value 중 최댓값
            max_combinatnios_dic_value = max(combinations_dic.values())
            # value가 1이면 넘어가기
            if value == 1 or not max_combinatnios_dic_value:
                continue
            # 가장 최댓값인 경우 key를 answer에 입력
            if value == max_combinatnios_dic_value:
                answer.append(key)
    # retrun 전에 오름차순 정렬하기
    answer.sort()
    return answer

```



## Comment

조합을 사용해서 푸는 문제.

문제에서 요구하는 메뉴의 수만큼에 해당하는 조합을 만들고 그 조합이 주어진 orders로부터, 얼마나 나오는지 카운트를 하고 최댓값만 답으로 출력해내면 된다.

반복문이 많이 나오게 되는데, 각 반복문의 시점에서 변수에 어떤 것이 담길 지 잘 파악해야 한다. 조합의 최댓값을 찾는 것에서 어떤 시점에서 찾을 수 있을지 잘 고심해봐야 한다.

조합을 만들 시, order를  정렬을 하지 않으면, 다른 조합으로 취급되어서 카운트가 제대로 되지 않는다. 반드시 sorted함수를 써서 파라미터를 넘겨야 한다.

답을 출력 전에도 사전 순으로 해야하므로 return 전에 sort메소드를 사용한다.

# Reference

[프로그래머스](https://programmers.co.kr)

