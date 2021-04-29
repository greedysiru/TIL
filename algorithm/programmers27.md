




# [프로그래머스] 위장 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 위장
def solution(clothes):
    answer = 1
    # 딕셔너리 변환
    clothes_dic = {}
    for cloth in clothes:
        # 키가 딕셔너리에 없는 경우
        # 배열안에 키 값을 넣기
        if cloth[1] not in clothes_dic:
            clothes_dic[cloth[1]] = [cloth[0]]
        # 키가 딕셔너리에 있는 경우
        # append하기
        else:
            clothes_dic[cloth[1]].append(cloth[0])
    # 입을 수 있는 옷 조합은
    # 옷 조합의 수 = (각 종류별 옷의 수 + 1) * (각 종류별 옷의 수 + 1) ... - 1
    # -1 은 전부 안 입었을 때의 경우의 수
    # +1은 해당 옷을 안 입었을 때의 경우의 수
    for cloth_dic in clothes_dic:
        answer *= len(clothes_dic[cloth_dic]) + 1
    answer -= 1
    return answer

```



## Comment

2차원 배열을 for문을 이용하여 딕셔너리로 변환하였다. 키가 딕셔너리에 존재하지 않으면 배열을 생성함과 동시에 키값을 넣었고 키가 딕셔너리에 존재하면 append로 처리하였다. 딕셔너리가 완성되면 모든 옷 조합의 수는 각 종류별 옷의 수들을 모두 곱한 값 -1이므로 for문을 이용해 구할 수 있었다.

# Reference

[프로그래머스](https://programmers.co.kr)

