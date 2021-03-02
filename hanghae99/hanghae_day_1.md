# [항해99 1기] [Chapter1] 웹개발 미니 프로젝트 (1) (2021.3.1)

# Git 시작하기

>  여러 사람들이 작업하는 코드를 한 곳에서 편하게 관리할 수 있게 해주는 프로그램

* 공동 작업시 발생할 수 있는 문제 상황 방지
* Git은 작업 기록을 남기고 이력을 추적해서 코드를 손쉽게 관리하도록 도와준다.
* 버전 관리도 매우 간편



## 인트로 - 이것만 알고 가기

* git을 사용하려면 작업자 컴퓨터들과 **가운데에서 코드를 관리할 원격저장소**가 있어야 한다.
  * 내 로컬 저장소에 작업 내역을 반영 -> **commit**
  * 원격 저장소에 작업 내역을 업로드 -> **push**
  * 원격 저장소 작업 내역을 내 로컬 저장소로 -> **pull**



### 자주 쓰이는 명령어 모음

`git init`: git repository를 내 컴퓨터에 생성

`git clone [url]`: 이미 있는 repositroy를 내 컴퓨터에 다운로드

`git add.`: 변경된 파일 모드를 커밋. 파일명/폴더명 입력 가능

`git commit -m [메시지]`: 내 컴퓨터에 변경 내용을 커밋

`git status`: 변경 상태 확인

`git pull`: 변경사항 다운로드

`git push origin master`: 마스터 브랜치에 푸시 하기

`git push origin [브랜치명]`: 특정 브랜치에 푸시하기

`git branch mybranch1`: 브랜치 만들기(mybranch1)

`git checkout mybranch1`: 브랜치로 이동하기(mybranch1)



# 셀레니움

## 01. 웹 스크래핑

> **웹 페이지에서 우리가 원하는 부분의 데이터를 수집해오는 것**

* **requests**로 페이지를 가져오고
* **beautifulsoup4**로 필요한 데이터를 추출



## 02. 동적인 웹 사이트

* 동적인 웹사이트를 스크래핑할 때는 브라우저에 띄운 후 소스코드를 가져오는 방법을 사용
  * ex) 멜론 차트처럼 실시간으로 좋아요  수가 바뀌는 경우



## 03. 셀레니움 설치

* 크롬 드라이버 다운로드
  * [설치](https://chromedriver.storage.googleapis.com/index.html)
  * 컴퓨터의 운영체제와 크롬 버전에 맞는 드라이버를 받기
* selenium 패키지 설치



### 예시

```python
from bs4 import BeautifulSoup
from selenium import webdriver
from time import sleep

driver = webdriver.Chrome('./chromedriver')  # 드라이버를 실행합니다.


url = "https://www.melon.com/chart/day/index.htm"
# headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.86 Safari/537.36'}
# data = requests.get(url, headers=headers)

driver.get(url)  # 드라이버에 해당 url의 웹페이지를 띄웁니다.
sleep(5)  # 페이지가 로딩되는 동안 5초 간 기다립니다. 

req = driver.page_source  # html 정보를 가져옵니다.
driver.quit()  # 정보를 가져왔으므로 드라이버는 꺼줍니다.

# soup = BeautifulSoup(data.text, 'html.parser')
soup = BeautifulSoup(req, 'html.parser')  # 가져온 정보를 beautifulsoup으로 파싱해줍니다.

songs = soup.select("#frm > div > table > tbody > tr")
print(len(songs))

for song in songs:
    title = song.select_one("td > div > div.wrap_song_info > div.rank01 > span > a").text
    artist = song.select_one("td > div > div.wrap_song_info > div.rank02 > span > a").text
    likes = song.select_one("td > div > button.like > span.cnt").text
    print(title, artist, likes)
```



## 04. 셀레니움 응용

* 셀레니움으로 다양한 동작을 할 수 있다.



### 스크롤 내리기

```python
driver.execute_script("window.scrollTo(0, 1000)")  # 1000픽셀만큼 내리기
```



### 맨 밑까지 내리기

```python
sleep(1)
driver.execute_script("window.scrollTo(0, document.body.scrollHeight);")
sleep(10)
```



# 네이버 지도 API

## 01. 네이버 클라우드 플랫폼

* [네이버 클라우드 플랫폼](https://www.ncloud.com/)
* 회원 가입 후 지도 API 이용 신청



## 02. 설정 정보 입력

* Application 이름: 영문, 숫자, - 조합
* Maps:  필요 서비스 선택
* WEB 서비스 URL
* 이후, 콘솔에서 인증정보 발급
  * 복사해 놓기



## 03. 지도 API 사용하기

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport"
              content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no">
        <title>간단한 지도 표시하기</title>
        <script type="text/javascript"
                src="https://openapi.map.naver.com/openapi/v3/maps.js?ncpClientId=YOUR_CLIENT_ID"></script>
        <script src=" https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>

        <style>
            #map {
                width: 100%;
                height: 400px;
            }
        </style>

        <script>
            $(document).ready(function () {
                let map = new naver.maps.Map('map', {
                    center: new naver.maps.LatLng(37.4981125, 127.0379399),
                    zoom: 10
                });
            })
        </script>
    </head>
    <body>
        <div id="map"></div>
    </body>
```

`YOUR_CLIENT_ID` 부분에 콘솔에서 확인한 인증 정보 넣기



# VSC Python 가상환경

* VSC에서 ctrl + `(백틱) 단축키로 터미널 킨 후 아래 명령어 입력

## 01. venv

```python
python3 -m venv .venv
```



## 02. 가상환경 들어가기/나가기

### 들어가기

```python
source .venv/bin/activate
```

### 나가기

```python
deactivate
```



## 03. pip

### pip 최신 버전 업그레이드

```python
pip install --upgrade pip
```



### 패키지 설치

* requests 설치 예시

```python
pip install requests
```



### 패키지 설지 확인

* requests 설치 확인 예시

```패키치 설치 확인
pip show requests
```

