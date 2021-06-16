# [프로그래머스] 베스트앨범 - python 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**



## 파이썬 코드

```python
# 베스트 앨범
def solution(genres, plays):
    answer = []
    # 주어진 곡의 갯수
    song_ea = len(genres)
    # genres, plays의 정보를 필요한 형태로 저장할 딕셔너리
    total_dic = {}
    # 곡의 갯수만큼 genres, plays의 각 인덱스에 접근하기
    for i in range(song_ea):
        # total_dic의 key에 장르가 없는 경우
        if genres[i] not in total_dic.keys():
            # 새로운 key를 생성하고 하위 딕셔너리 만들기
            # 하위 딕셔너리에 장르 별 총 재생수를 입력할 total key 생성 후 plays[i] 넣기
            # 곡 번호를 key로하고 plays[i] 넣기
            total_dic[genres[i]] = {'total': plays[i], i: plays[i]}
        # key가 존재하는 경우
        else:
            # total에 합 누적
            total_dic[genres[i]]['total'] += plays[i]
            # 곡 번호에 plays[i] 입력
            total_dic[genres[i]][i] = plays[i]
    # 만들어진 total_dic의 items으로 정렬하기
    # 각 genre의 하위 딕셔너리의 total key를 기준으로 내림차순 정렬
    sorted_genres_list = sorted(
        total_dic.items(), key=lambda x: x[1]['total'], reverse=True)
    # total을 기준으로 정렬한 리스트의 한 요소씩 접근
    for j in range(len(sorted_genres_list)):
        # 각 장르의 딕셔너리를 가져오기
        genre_dic = sorted_genres_list[j][1]
        # 가져온 각 장르의 딕셔너리에서 각 value를 기준으로 내림차순 정렬하기
        sorted_songs_list = sorted(
            genre_dic.items(), key=lambda x: x[1], reverse=True)
        # 두 개씩 answer 리스트에 넣기
        k = 1
        while k <= 2:
            answer.append(sorted_songs_list[k][0])
            # 리스트의 길이가 3미만인 경우 중단
            # total까지 포함되어 있는 리스트이므로 2일 때 total과 곡 1개의 play 수가 있으므로
            if (len(sorted_songs_list) < 3):
                break
            k += 1
    return answer
```



## Comment

주어진 두 정보를 for문으로 접근하며 필요한 형태로 딕셔너리로 전환하는 것은 비교적 수월하게 하였다. 딕셔너리의 형태는 장르 명을 가장 상위의 key로 하고 각 장르의 key value로는 장르의 총 재생수인 total 그리고 장르에 속한 곡번호와 재생수를 입력하도록 하였다.

딕셔너리의 value를 기준으로 정렬을 하려면, lambda를 사용해야 한다. lambda의 사용법은 매번 잊어버려서 docs를 보며 적용하였다. 만들어진 total_dic을 items 메소드로 딕셔너리에 존재하는 요소들을 리스트로 나열하고 lambda의 key로   total을 지정하여 total을 기준으로 내림차순 정렬하도록 하였다. 정렬 후에 다시 각 장르의 하위 딕셔너리에 접근하여 곡 재생수를 기준으로 내림차순 정렬하였고 장르별로 두 곡씩 answer 리스트에 append하였다.

다른 분들의 답안을 보니, 나와 비슷하게 장르를 기준으로 최상위 key를 지정하였다. 그러나, 각 장르의 하위에는 리스트나 튜플로 데이터를 입력하였다. 확실히 튜플이나 리스트로 입력을 한다면, 정렬할 때 더 수월할 것 같다.

# Reference

[프로그래머스](https://programmers.co.kr)

