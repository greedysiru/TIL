# [프로그래머스] 방금그곡 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 방금그곡
import math

# #이 붙은 문자를 치환하는 함수

def replace_string(string):
    return string.replace('C#', 'c').replace('D#', 'd').replace('F#', 'f').replace('G#', 'g').replace('A#', 'a')

def solution(m, musicinfos):
    #  #이 붙은 문자 치환하기
    m = replace_string(m)
    answer = ['(None)', 0]
    # 기억한 멜로디 문자열의 길이
    m_len = len(m)
    # 입력받은 곡의 갯수
    songs_ea = len(musicinfos)
    # 한 곡씩 접근하여 기억한 멜로디와 비교하기
    for i in range(songs_ea):
        # 곡 정보를 ,를 기준으로 나누기
        song = musicinfos[i].split(',')
        # 곡의 재생 시간
        song_play_time = (int(song[1][:2]) * 60 + int(song[1][3:])) - \
            (int(song[0][:2]) * 60 + int(song[0][3:]))
        # 곡의 제목
        song_title = song[2]
        # 곡의 멜로디
        song_m = replace_string(song[3])
        # 곡의 멜로디 길이
        song_m_len = len(song_m)
        # 실제 실행된 멜로디 만들기
        # 곡이 반복된 횟수 (올림)
        song_m_repeated_count = math.ceil(song_play_time / song_m_len)
        # 멜로디를 올림한 곡이 반복된 횟수만큼 반복하고 재생시간만큼 슬라이싱하기
        played_m = (song_m * song_m_repeated_count)[:song_play_time]
        # 만들어진 멜로디와 기억한 멜로디 비교
        if m in played_m and answer[1] < song_play_time:
            answer[0] = song_title
            answer[1] = song_play_time
    return answer[0]
```



## Comment

기억하고 있는 멜로디와 주어진 곡 정보들을 비교하여 맞는 곡 제목을 찾아내는 문제. 문자열을 하나하나 비교해야하는데, 여기서, #이 들어간 음은 하나의 문자로 취급해야한다. 문자를 치환하는 함수를 선언하여 replace메소드를 사용해서 소문자 알파벳으로 치환해준다.

주어진 곡 정보들은 리스트의 형태로, 각 요소는 콤마(,)를 기준으로 재생 시작 시간, 재생 끝 시간, 이름, 멜로디로 구성되어있다.  split메소드로 나누어서 적절한 변수에 할당한다. 그리고 재생 시작 시간과 재생 끝 시간의 차이를 구하여 재생 시간을 구해야 하는데, 시간의 단위를 고려하여 계산한다.

구한 재생시간을 이용해서, 각 곡의 멜로디를 반복한다. 재생시간을 멜로디 길이로 나누어 math모듈의 ceil로 올림하여 그 만큼 멜로디를 반복하게 한다. 그리고 재생시간만큼 리스트 슬라이싱하여 실제로 재생된 멜로디를 구할 수 있다.

멜로디가 포함된 곡이 복수인 경우, 재생 시간이 긴 음악 제목을 출력하는 것이므로, answer에 0번 인덱스에는 음악 제목을 1번 인덱스에는 재생 시간을 입력하도록 하고 재생시간이 최대값일 경우에만 최신화를 하도록 조건문을 넣어준다.

카카오문제는 지문을 꼼곰히 읽어봐야한다. 혼자 풀었을 때, #이 붙은 문자 처리를 간과하여 많은 시간을 투자해야만 했다.

# Reference

[프로그래머스](https://programmers.co.kr)

