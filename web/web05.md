# [스파르타코딩] 웹개발 종합반 항해 1기 3주차 (1)(2021.2.3)



**상세 내용 [블로그](https://greedysiru.tistory.com/160) 참고**



# 1. 파이썬 시작하기

* 파이썬을 설치한다는 것의 의미
  * 일종의 번역팩을 설치
  * 파이썬 문법으로 된 것을 이진법 코드로 변환할 수 있도록 한다.



# 2. 파이썬 기초공부

## 변수 & 기본연산

```python
a = 3;
b = a;
a = a + 1;

num1 = a * b;
num2 = 99
```

* 변수에는 숫자, 문자형, 리스트 형, 딕셔너리 형, 딕셔너리와 리스트의 조합, 불리언 등이 들어갈 수 있다.



## 자료형

* 숫자, 문자형: 문자형은 콤마('')로 표현
* 리스트형: 대괄호([]) 사용
  * **.append()** : 리스트의 뒤에 원소 추가
* Dictionary 형: 중괄호({}) 사용

> a = { 'name' : 'bob', 'age' : 21 }

* Dictionary와 List형은 서로 조합될 수 있다.

  > people = [{'name':'bob','age':20},{'name':'carry','age':38}]



## 함수

> def 함수명 (받을 인자):
>
> ​    실행할 코드

* 실행할 코드는 **들여쓰기**로 구분한다.



## 조건문

> if 조건 :
>
> ​    실행할 코드
>
> else:
>
> ​    실행할 코드

* 실행할 코드는 **들여쓰기**로 구분한다.



## 반복문

* 파이썬에서, 반복문은 리스트의 요소들을 하나씩 꺼내 사용할 수 있다.

```python
fruits = ['사과', '배', '감', '귤'];

for a in frunits:
    print(a);
# 배열 fruits의 요소들이 변수 a에 하나하나 입력된다.
# 사과, 배, 감, 귤 출력
```



# 3. 파이썬 패키지 설치하기

## 패키지, 라이브러리

* Python에서 **패키지**는 모듈(기능 묶음)을 모아 놓은 단위이다.
* 이런 **패키지의 묶음**을 **라이브러리**라고 한다.



## 가상환경

* **프로젝트별 공구함**
* 같은 시스템에서 실행되는 다른 파이썬 응용 프로그램들의 동작에 영향을 주지 않기 위해서 파이썬 배포 패키지들을 설치하거나 업그레이드하는 것을 가능하게 하는 **격리된 실행 환경**



# 4. 패키지 사용해보기

## requests 라이브러리

```python
import requests # requests 라이브러리

r = requests.get('url') # API url
```





## 서울시 미세먼지

* Requests 라이브러리를 사용하여 서울시에서 미세먼지 지수가 50 초과한 지역 출력하기

```python
import requests # requests 라이브러리

r = requests.get('http://openapi.seoul.go.kr:8088/6d4d776b466c656533356a4b4b5872/json/RealtimeCityAir/1/99')
rjson = r.json() # API를 가져와서 json을 별도의 변수에 저장

gus = rjson['RealtimeCityAir']['row'] # 서울시 각 구마다의 미세먼지 정보 가져오기

for gu in gus: # 서울시의 모든 구의 미세먼지 정보로부터 반복문으로 하나씩 접근
    gu_name = gu['MSRSTE_NM']; # 구의 이름 정보
    gu_mise = gu['IDEX_MVL']; # 구의 미세먼지 정보
    if (gu_mise > 50):       # 구의 미세먼지 지수가 50초과 시 해당 구의 이름과 미세먼지 지수 출력
        print(gu_name,gu_mise);
```



# 5. 웹스크래핑(크롤링) 기초

## beautifulsoup4 라이브러리

* 웹스크래핑(크롤링)을 할 수 있는 라이브러리
* 파이참에서 **bs4** 설치 후 사용

```python
import requests
from bs4 import BeautifulSoup

headers = {'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.86 Safari/537.36'} # 코드단에서 접근할 수 있도록 함
data = requests.get('url',headers=headers) # 원하는 곳의 url

# HTML을 BeautifulSoup이라는 라이브러리를 활용해 검색하기 용이한 상태로 만듦
# soup이라는 변수에 "파싱 용이해진 html"이 담긴 상태가 됨
# 이제 코딩을 통해 필요한 부분을 추출하면 된다.
soup = BeautifulSoup(data.text, 'html.parser')
```



## select & select_one

```python
# 선택자를 사용하는 방법 (copy selector)
soup.select('태그명')
soup.select('.클래스명')
soup.select('#아이디명')

soup.select('상위태그명 > 하위태그명 > 하위태그명')
soup.select('상위태그명.클래스명 > 하위태그명.클래스명')

# 태그와 속성값으로 찾는 방법
soup.select('태그명[속성="값"]')

# 한 개만 가져오고 싶은 경우
soup.select_one('위와 동일')
```



## 네이버 영화 페이지에서 영화 제목 가져오기

```python
import requests
from bs4 import BeautifulSoup

headers = {'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.86 Safari/537.36'}
data = requests.get('https://movie.naver.com/movie/sdb/rank/rmovie.nhn?sel=pnt&date=20200303',headers=headers)

soup = BeautifulSoup(data.text, 'html.parser')

movies = soup.select('#old_content > table > tbody > tr')

# movies (tr들) 의 반복문을 돌리기
for movie in movies:
    # movie 안에 a 가 있으면,
    a_tag = movie.select_one('td.title > div > a')
    if a_tag is not None:                                       # None 제외하기
        rank = movie.select_one('td:nth-child(1) > img')['alt'] # img 태그의 alt 속성값을 가져오기
        title = a_tag.text                                      # a 태그 사이의 텍스트를 가져오기
        star = movie.select_one('td.point').text                # td 태그 사이의 텍스트를 가져오기
        print(rank,title,star)
```

* 웹 페이지마다 html 태그의 방식이 다르므로 상황에 맞게 전략을 세운다.
* 이 경우, **None을 제외하고 출력**하도록 한다.
* 크롬 개발자 도구에서 **Copy selector**를 사용하여 필요한 선택자를 추출한다.

# Reference

**스파르타코딩 - 웹개발 종합반**