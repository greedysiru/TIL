# [프로그래머스] 추석 트래픽 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 추석 트래픽
# 첫시간, 끝시간 각각으로부터 1초가 경과되었을 때 포함되는 로그 구하기
def get_cnt(time, lines_start_and_end):
    cnt = 0
    start = time
    # 1초 경과
    end = time + 1
    # 시작시간과 끝시간이 있는 2차원 리스트 하나씩 접근
    for start_and_end in lines_start_and_end:
        # 끝시간이 start보다 이후일 때는 포함
        # 시작시간이 end보다 이전일 때도 포함
        if start_and_end[1] >= start and start_and_end[0] < end:
            cnt += 1
    return cnt


def solution(lines):
    answer = 0
    # 각 로그의 시작, 끝을 구하기
    lines_start_and_end = []
    # 입력받은 lines에서 필요한 정보만 빼내기
    for log in lines:
        # 공백을 기준으로 나누기
        # [0]: 날짜, [1]: 시간 [2]: 경과 시간
        time = log.split(' ')
        # 끝나는 시간을 콜론을 기준으로 나누기
        time_end = time[1].split(':')
        # 시간, 분을 초 단위로 변환
        end_second = (float(time_end[0]) * 60 * 60) + \
            (float(time_end[1]) * 60) + float(time_end[2])
        # 처리 시간을 s를 제외하고 실수화
        processing_time = float(time[2].split('s')[0])
        # 끝나는 시간 - 처리 시간의 결과를 소수 셋째 자리까지 반올림 후, 0.001초 더하기
        # 처리시간은 시작시간과 끝 시간을 포함하므로
        start_second = round((end_second - processing_time), 3) + 0.001
        # 각 로그의 시작,끝을 초단위로 각 인덱스에 넣기 (2차원 리스트)
        lines_start_and_end.append([start_second, end_second])

    # 만들어진 2차원 리스트를 하나씩 접근
    for start_and_end in lines_start_and_end:
        # 최대 수 구하기
        # 시작시간 + 1초 , 끝시간 + 1초 각 경우와 기존의 answer 값에서 최대값이 answer를 최신화
        answer = max(answer, get_cnt(start_and_end[0], lines_start_and_end), get_cnt(
            start_and_end[1], lines_start_and_end))
    return answer
```



## Comment

역시 어려웠던 카카오 기출문제.

주어진 데이터를 하나씩 접근해서 문제 해결에 도움이 되는 포맷으로 변환하는 것이 핵심이다.

split을 활용해서 문자열을 나누고 실수화를 하여 계산을 할 수 있도록 초 단위로 시작시간과 끝시간을 변환하였다. 그 이후 2차원 리스트의 형태로 각 로그가 시작되는 시간, 끝나는 시간을 초단위로 입력하였다.

그 이후, 시작 시간 + 1초, 끝나는 시간 + 1초의 각 경우에서 각 로그의 시작과 끝이 걸쳐있는지를 판별하여 카운트하는 함수를 만들었고 최댓값이 답으로 출력되도록 하였다.

# Reference

[프로그래머스](https://programmers.co.kr)

