# [항해99 1기] [Chapter1] 웹개발 미니 프로젝트 (3) (2021.3.3)



## 스크래핑

### 생생정보통 맛집 스크래핑

* 파이썬 코드

```python
from selenium import webdriver # 셀레니움, bs4
from bs4 import BeautifulSoup
import time
from selenium.common.exceptions import NoSuchElementException
from pymongo import MongoClient
import requests

# localhost의 foodlist에 저장하기
client = MongoClient('localhost', 27017)
db = client.foodlist

driver = webdriver.Chrome('./chromedriver')

# 생생정보통 맛집 스크래핑
url = "https://menutong.com/bbs/board.php?bo_table=sangto"

driver.get(url)
time.sleep(5)

# 더 많은 페이지 크롤링
for i in range(4, 13):

    req = driver.page_source

    soup = BeautifulSoup(req, 'html.parser')

    # 각 식당에 해당하는 카드 선택
    places = soup.select("#list-body > div")
    print(len(places))

    # 식당 이미지 src, href, 이름, 카테고리, 번호, 주소 가져오기
    for place in places:
        img = place.find('img')
        img_src = img['src']
        a = place.find('a')
        a_href = a['href']
        title = place.select_one(
            "div.list-text > div.list-text > div.text-muted.font-12 > font:nth-child(2) > b").text
        category = place.select_one(
            "div.list-text > div.list-text > div.text-muted.font-12 > font:nth-child(5) > b").text
        tel = place.select_one(
            "div.list-text > div.list-text > div.text-muted.font-12 > span:nth-child(7)").text
        address = place.select_one(
            "div.list-text > div.list-text > div.text-muted.font-12 > span:nth-child(9)").text

        # 문자열 인덱싱
        address = address[5:]

        # foodlist DB에 저장
        doc = {
          "title": title,
          "address": address,
          "category": category,
          "img_src": img_src,
          "a_href": a_href,
          "tel": tel
           }
        db.foodlist.insert_one(doc)

    btn_more = driver.find_element_by_css_selector(
        "#fboardlist > div.list-page.text-center > ul > li:nth-child(%d) > a" % (i))
    btn_more.click()
    time.sleep(5)
driver.quit()
```



### 더 많은 페이지 가져오기

* 내가 가져올 웹 페이지는 하단에 목록버튼이 있는 방식이었다.
* 스크래핑 작업을 for문으로 반복
* 매 작업의 스크래핑이 끝나면 명령문이 끝나기 전에 driver로 버튼을 찾아 클릭한다.
  * 요소 검사로 목록이 올라갈 때 어떤 부분이 달라지는 지 분석
  * 반복문의 i를 활용



### 문자열 슬라이싱

* 가져온 데이터에 필요없는  공통 부분을 덜어내서 필요한 부분만 뽑아낸다.



### 태그 찾기

* 필요한 태그를 찾고 속성을 뽑을 수 있다.

```python
img = place.find('img')
img_src = img['src']
```



## jinja2로 페이지 구성하기

### flask에서 데이터 넘기기

```python
@app.route('/resultpage')
def main():
    foodlist = list(fooddb.foodlist.find({}, {"_id": False}))
    return render_template("result.html", foodlist = foodlist)
```



### 전달받은 데이터를 활용하여 페이지 구성

```html
<div class="food_list">
    <span class="food_list_main_title">더 많은 메뉴를 추천드립니다!</span>
    {% for list in foodlist %}
    {% set list_href = list["a_href"] %}
    {% set list_img = list["img_src"] %}
    {% set list_title = list["title"] %}
    {% set list_category = list["category"]%}
    {% set list_address = list["address"] %}
    {% set select_address = list_address[0:2] %}
    {% if select_address == "서울" %}
    <div class="rows hovereffect">
      <a href="{{list_href}}" class="food_list_a" target="_blank">
        <div class="col">
          <img src="{{list_img}}" class="food_list_pic">
        </div>

        <div class="col_text"> <span class="food_list_title">{{list_title}}</span>
          <span class="food_list_category">{{list_category}}</span> <span
            class=food_list_address>{{list_address}}</span>
        </div>
      </a>
    </div>
    {% endif %}
    {% endfor %}
```



## jinja 문법 정리

### 변수 선언

```jinja2
{% set list_href = list["a_href"] %}
```



### 반복문

```jinja2
{% for list in foodlist %}
{% endfor %}
```



### if문

```jinja2
{% if select_address == "서울" %}
{% endif %}
```



## flask 팁

* ajax의 호출과 flask의 응답을 짝을 잘 맞출것

```python
@app.route('/result', methods=["GET"])
def get_result():
    foods = list(fooddb.foodlist.find({}, {"_id": False}))

    return jsonify({'result': 'success', 'foods': foods})
```

```javascript
function get_food() {
      $.ajax({
        type: "GET",
        url: '/result',
        data: {},
        success: function (response) {
          let foods = response["foods"]
          // 난수 생성 후 랜덤 음식점 가져오기
          let num = foods.length
          let random = Math.floor(Math.random() * num);
          let food = foods[random]
          // 음식 결과 출력 함수 호출
          food_info(food)
        }
      }
      );
    }
```

method와 url의 짝을 꼭 잘 맞춰야 한다!



## pymongo 팁

```python
client = MongoClient('localhost', 27017)
db = client.member
fooddb =client.foodlist
```

localhost의 mongoDB를 client에 담아오는 것이다.

각각 필요한 db를 호출해주면 된다.



## decode 오류

jwt를 통해서 토큰을 발급 받은 후

```javascript
token = jwt.encode(payload, SECRET_KEY, algorithm='HS256').decode('utf-8')
```

*  **AttributeError: 'str' object has no attribute 'decode'** 오류가 발생하는 경우
  * python3로 실행하기 때문에 발생
* python3는 utf-8이기 때문에 .decode 부분을 지워야 한다.
* jwt버전을 1.7.1로 내려도 해결가능하다.