


# [프로그래머스] 체육복 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 파이썬 코드

```python
# 체육복
def solution(n, lost, reserve):
    # 빌리기전 체육복을 가진 학생 수 = 총학생수 - 잃은 학생수
    left = n - len(lost)
    # 빌린 학생수를 담을 변수
    borrowed = 0
    # 여분의 체육복이 있는 학생을 제외한 수업을 듣지 못하는 학생
    real_lost = []

    # 잃어버린 학생 리스트를 대상으로 입을 수 있는 체육복 사이즈가 reserve에 있는 것을 확인
    # 잃어버린 학생 리스트 하나씩 접근
    for i in range(len(lost)):
        # 확인 전에 여벌 체육복의 도난여부를 확인하고 도난당한 경우 빌려줄 수 없으므로 예외처리
        # lost 리스트에서도 수업을 들을 수 있는 학생이므로 real_lost에 넣기
        if lost[i] in reserve:
            reserve.remove(lost[i])
            # 체육복 남은수 1 더해주기
            left += 1
            continue
        if lost[i] not in reserve:
            real_lost.append(lost[i])
    for j in range(len(real_lost)):
        # 입을 수 있는 체육복 확인
        #  한 치수 큰 것을 확인
        if (real_lost[j] + 1) in reserve:
            reserve.remove(real_lost[j] + 1)
            borrowed += 1
        # 한 치수 작은 것을 확인
        elif (real_lost[j] - 1) in reserve:
            reserve.remove(real_lost[j] - 1)
            borrowed += 1

    # 답 구하기
    answer = left + borrowed
    return answer
```



## Comment

잃어버린 학생과 여분을 가진 학생을 고려해서 풀어야 한다. 그 이후에는 실질적으로 빌려야하는 학생(체육복이 없는)이 입을 수 있는 치수가 여분을 가진 학생 리스트에 있는지 확인하면 된다.

어찌저찌 풀었는데 모범답안보고 충격먹었다... 내 코드 길이의 반의 반정도 길이로 풀어낸 것을 볼 수 있었다 ^^...

리스트 컴프리헨션의 강력함을 몸소 느꼈다.

이외의 풀이로는 set 집합 자료형을 사용하여 차집합으로 쉽게 풀 수도 있다.

뺑돌아가는 나...

# Reference

[프로그래머스](https://programmers.co.kr)

