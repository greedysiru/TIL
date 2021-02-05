# [스파르타코딩] 웹개발 종합반 항해 1기 4주차 (2)(2021.2.4 ~ 5)



**상세 내용 [블로그](https://greedysiru.tistory.com/166) 참고**

# 모두의 책 리뷰

# 1. POST 연습(리뷰 저장)

* 클라이언트의 입력을 받아 저장하는 API 만들기
* **Create -> POST**



## 1. 클라이언트와 서버 확인

> 1. 요청 정보 : 요청 URL = **/review**, 요청방식 = **POST**
> 2. 서버가 제공할 기능 : 클라이언트에게 정해진 메시지를 보낸다.
> 3. 응답 데이터 : (JSON 형식) 'result' = 'success', 'msg' =' 리뷰가 성공적으로 작성되었습니다.'



### 서버 코드 - app.py

```python
@app.route('/review', methods=['POST'])
def write_review():
    return jsonify({'result': 'success', 'msg': '리뷰가 성공적으로 작성되었습니다.'})
```

* 클라이언트로부터 **/review , POST**로 입력을 받았을 때 **함수 write_review()** 호출
* 함수는 **리뷰 성공 메시지를 return**

### 클라이언트 코드 - index.html

```Javascript
function makeReview() {
    $.ajax({
        type: "POST",
        url:  "/review",
        data: { },
        success: function (response) {
            if (response["result"] == "success") {
                alert(response["msg"] );
                window.location.reload();
            }
        }
    })
}
```

* 서버에게 **/review, POST**로 보내기
* 서버에게 **response**를 받는것을 성공(**success**)하면, 경고창으로 **성공 메시지를 출력**
* 그 이후 **페이지를 리로드**



## 2. 서버부터 만들기

* 클라이언트로부터 **title, author, review를 받아 저장하는 API 만들기**
* API 정보

> 1. 요청 정보
>    - 요청 URL = **/review**, 요청 방식 =  **POST**
>    - 요청 데이터: 제목(title), 저자(author), 리뷰(review)
> 2. 서버가 제공할 기능 : 클라이언트에게 보낸 요청 데이터를 데이터베이스에 생성(Create) 후, 응답 데이터 보냄
> 3. 응답 데이터: (JSON)형식 'msg' = '리뷰가 성공적으로 작성되었습니다.'



### 서버 코드 - app.py

```python
@app.route('/review', methods=['POST'])
def write_review():
    title_receive = request.form['title_give']
    author_receive = request.form['author_give']
    review_receive = request.form['review_give']

    doc = {
        'title': title_receive,
        'author': author_receive,
        'review': review_receive
    }
    db.bookreview.insert_one(doc)
    return jsonify({'msg': '리뷰가 성공적으로 작성되었습니다.'})
```

* 클라이언트로부터 **title, author, review 를 가져온다.**
* 가져온 정보들을 이용해서 **DB에 삽입할 딕셔너리를 만든다.**
* **딕셔너리를 DB에 삽입**
* **성공 메시지 반환**



## 3. 클라이언트 만들기

* API를 사용할 클라이언트를 만든다.
* 리뷰를 작성하기 위해 필요한 정보: title, author, review

> 1. input에서 title, author, review 가져오기
> 2. 입력값이 하나라도 없을 때 alert 띄우기
> 3. Ajax로 서버에 요청하고 화면 다시 로딩



### 클라이언트 코드 - index.html

```Javascript
function makeReview() {
    // 화면에 입력어 있는 제목, 저자, 리뷰 내용을 가져옵니다.
    let title = $("#title").val();
    let author = $("#author").val();
    let review = $("#bookReview").val();

    // POST /review 에 저장(Create)을 요청합니다.
    $.ajax({
        type: "POST",
        url: "/review",
        data: { title_give: title, author_give: author, review_give: review },
        success: function (response) {
            alert(response["msg"]);
            window.location.reload();
        }
    })
}
```

* input, textarea로부터 **title, author, review를 가져온다.**
* **POST, /reveiw**에 **data**를 보내고 저장을 요청
* 저장이 성공하면, **메시지 alert 후 페이지 리로드**



# 2. GET 연습(리뷰 보여주기)

* 저장된 리뷰를 화면에 보여주기
* **Read -> GET**



## 1. 클라이언트와 서버 확인하기

> 1. 요청 정보 : 요청 URL = /review, 요청 방식 = GET
> 2. 서버가 제공할 기능 : 클라이언트에게 정해진 메시지를 보냄
> 3. 응답 데이터 : (JSON 형식) {'msg': '이 요청은 GET!'}



### 서버 코드 - app.py

```python
@app.route('/review', methods=['GET'])
def read_reviews():
    sample_receive = request.args.get('sample_give')
    print(sample_receive)
    return jsonify({'msg': '이 요청은 GET!'})
```

* 클라이언트로부터 **/review , GET**으로 입력을 받았을 때 **함수 read_review()** 호출
* 함수는 **로드 성공 메시지를 return**



### 클라이언트 코드 - index.html

```Javascript
function showReview() {
		$.ajax({
        type: "GET",
        url: "/review?sample_give=샘플데이터",
        data: {},
        success: function (response) {
            alert(response["msg"]);
        }
    })
}
```

* 서버에게 **/review, GET**으로 보내기
* 서버에게 **response**를 받는것을 성공(**success**)하면, 경고창으로 **성공 메시지를 출력**



## 2. 서버부터 만들기

* 클라이언트로에게 **리뷰 보여주는 API 만들기**
* API 정보

> 1. 요청 정보
>    - 요청 URL = **/review**, 요청 방식 =  **GET**
>    - 요청 데이터: 없음
> 2. 서버가 제공할 기능 : 데이터베이스에 리뷰 정보를 조회(Read)하고, 성공 메시지와 리뷰 정보를 응답 데이터로 보냄
> 3. 응답 데이터: (JSON)형식 'result' = 'success', 'reviews' = 리뷰리스트



### 서버 코드 - app.py

```python
@app.route('/review', methods=['GET'])
def read_reviews():
    reviews = list(db.bookreview.find({}, {'_id': False}))
    return jsonify({'all_reviews': reviews})
```

* **DB로부터 모든 리뷰 정보를 reviews에 가져온다.**
* **딕셔너리의 형태로 return**



## 3. 클라이언트 만들기

* 리뷰 목록을 서버에 요청하는 클라이언트를 만들기

> 1. 리뷰 목록을 서버에 요청하기
> 2. 요청 성공 여부 확인하기
> 3. 요청 성공했을 때 리뷰를 올바르게 화면에 나타내기



### 클라이언트 코드 - index.html

```Javascript
function showReview() {
                $.ajax({
                    type: "GET",
                    url: "/review",
                    data: {},
                    success: function (response) {
                        let reviews = response['all_reviews']
                        for (let i = 0; i < reviews.length; i++) {
                            let title = reviews[i]['title']
                            let author = reviews[i]['author']
                            let review = reviews[i]['review']

                            let temp_html = `<tr>
                                                <td>${title}</td>
                                                <td>${author}</td>
                                                <td>${review}</td>
                                            </tr>`
                            $('#reviews-box').append(temp_html)
                        }
                    }
                })
            }
```

* **서버에게 모든 리뷰 정보를 받아온다.**
* **반복문으로 모든 리뷰 정보로부터 title, author, review를 하나씩 받아온다.**
* 하나씩 받아온 리뷰 정보들을 **html 태그로서 append**



# 나홀로 메모장

# 1. API 설계하기

* 코딩을 하기 전에, 필요한 API를 설계한다.

## 포스팅API - 카드 생성(Create)

* 요청 정보
  * 요청 URL = /memo, 요청 방식 = POST
  * 요청 데이터 : URL(url_give), 코멘트(comment_give)
* 서버가 제공할 기능
  * URL의 meta태그 정보를 바탕으로 제목, 설명, 이미지URL 스크래핑
  * (제목, 설명, URL, 이미지URL, 코멘트) 정보를 모두 DB에 저장
* 응답 데이터
  * API가 정상적으로 작동하는지 클라이언트에게 알려주기 위해서 성공 메시지 보내기
  * (JSON 형식) 'result' = 'success'



## 리스팅 API - 저장된 카드 보여주기(Read)

* 요청 정보
  * 요청 URL = /memo, 요청 방식 = GET
  * 요청 데이터 : 없음
* 서버가 제공할 기능
  * DB에 저장되어있는 모든 (제목, 설명, URL, 이미지URL,  코멘트) 정보를 가져오기
* 응답 데이터
  * 아티클(기사)들의 정보(제목, 설명, URL, 이미지URL, 코멘트) -> 카드 만들어서 붙이기
  * (JSON 형식) 'articles': 아티클 정보



# 2. 조각 기능 구현해보기

* 익숙하지 않은 기능은 따로 파일을 만들어 실행해본다.
* 기사URL만 입력했을 때, 자동으로 기사 제목, 썸네일 이미지, 내용이 불러와진다.
  * **이는 meta태그를 크롤링함으로써 얻을 수 있다.**



## meta 태그

* HTML에서, 눈에 보이는 body외에 **사이트를 속성을 설명하는 태그**
* **head 부분에 들어간다.**
* 구글 검색 시 표시되는 설명문, 사이트 제목, 카톡 공유 시 표시 될 이미지 등



## meta 태그 스크래핑 하기

```python
import requests
from bs4 import BeautifulSoup

url = 'https://movie.naver.com/movie/bi/mi/basic.nhn?code=171539' # meta태그를 가져올 url

headers = {'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.86 Safari/537.36'}
data = requests.get(url,headers=headers)

soup = BeautifulSoup(data.text, 'html.parser') # 해당 url의 html을 가져오기

title = soup.select_one('meta[property="og:title"]')['content'] # meta 태그의 컨텐츠 가져오기
image = soup.select_one('meta[property="og:image"]')['content']
desc = soup.select_one('meta[property="og:description"]')['content']

print(title, image, desc)
```

* meta 태그를 크롬 개발자 도구를 이용해서 선택자를 가져와도 스크래핑이 안된다.
  * **파이썬 코드가 접속했을 때 나오는 meta 태그 순서가 다르기 때문이다.**
* **meta[property="og:title"]** 으로 스크래핑 할 수 있다.



# 3. POST 연습(메모하기)

* 클라이언트의 입력을 받아 DB에 저장하기
* **Create -> POST**



## 1. 클라이언트와 서버 확인하기

### 서버 코드 - app.py

```python
@app.route('/memo', methods=['POST'])
def post_articles():
		sample_receive = request.form['sample_give']
		print(sample_receive)
    return jsonify({'msg': 'POST 연결되었습니다!'})
```

* 클라이언트로부터 **/memo , POST**로 입력을 받았을 때 **함수 post_articles()** 호출
* **함수 실행 후 연결 메시지 return**

### 

### 클라이언트 코드 - index.html

```javascript
function postArticle() {
  $.ajax({
    type: "POST",
    url: "/memo",
    data: {sample_give:'샘플데이터'},
    success: function (response) { // 성공하면
      alert(response['msg']);
      window.location.reload();
    }
  })
}

<button type="button" class="btn btn-primary" onclick="postArticle()">기사저장</button>
```

* **클라이언트가 button을 클릭하면 함수 postArticle() 실행**
* 서버에게 **/memo, POST**로 보내기
* 서버에게 **response**를 받는것을 성공(**success**)하면, 경고창으로 **연결 메시지를 출력**
* 그 이후 **페이지를 리로드**



## 2. 서버부터 만들기

* 메모를 작성하기 위해 서버가 전달받아야 하는 정보
  * **URL(url_give)**
  * **코멘트(comment_give)**
* 이후 **URL**의 **meta 태그를** 스크래핑한 뒤 데이터를 **저장(Create)**
  * **URL(url)**
  * **제목(title)**
  * **설명(desc)**
  * **이미지 URL(image)**
  * **코멘트(comment)**
* 서버 로직
  1. 클라이언트로부터 데이터를 받기
  2. meta 태그를 스크래핑
  3. mongo DB에 데이터 넣기



### 서버 코드 - app.py

```python
## API 역할을 하는 부분
@app.route('/memo', methods=['POST'])
def saving():
    url_receive = request.form['url_give']
    comment_receive = request.form['comment_give']

## 스크래핑
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64)AppleWebKit/537.36 (KHTML, like Gecko) Chrome/73.0.3683.86 Safari/537.36'}
    data = requests.get(url_receive, headers=headers)
    soup = BeautifulSoup(data.text, 'html.parser')
    title = soup.select_one('meta[property="og:title"]')['content']
    image = soup.select_one('meta[property="og:image"]')['content']
    desc = soup.select_one('meta[property="og:description"]')['content']

#DB insert
    doc = {
        'title':title,
        'image':image,
        'desc':desc,
        'url':url_receive,
        'comment':comment_receive
    }

    db.articles.insert_one(doc)

    return jsonify({'msg':'저장이 완료되었습니다.'})
```

* 클라이언트로부터 **url_receive, comment_receive**를 받아온다.
* 받아온 **url**에 들어가서 **meta 태그**의 **og:title, og:image, og:description**을 스크래핑
* **스크래핑한 데이터들**을 **mongoDB의 articles에 저장**
* 완료 후 **클라이언트에게 저장 완료 return**



## 3. 클라이언트 만들기

* 메모를 작성하기 위해 서버에게 줄 정보
  * **URL(url_give)** : meta 태그를 가져올 url
  * **comment(comment_give)** : 유저가 입력한 코멘트
* 클라이언트 로직
  1. 유저가 입력한 데이터를 #post-url과 #post-comment에서 가져오기
  2. /memo에 POST 방식으로 메모 생성 요청
  3. 성공 시 페이지 새로고침



### 클라이언트 코드 - index.html

```Javascript
function postArticle() {
  let url = $('#post-url').val();
  let comment = $('#post-comment').val();
  $.ajax({
    type: "POST",
    url: "/memo",
    data: {url_give:url, comment_give:comment},
    success: function (response) { // 성공하면
      alert(response["msg"]);
      window.location.reload();
    }
  })
}
```

* **#post-url, #post-comment**로부터 **url과 comment** 받아오기
* **ajax**로 **서버**에게 **url_give, comment_give 전송**
* 서버에게 전송 후 **저장 완료를 return받으면, alert으로 출력**
* 그 이후 페이지 리로드



# 4. GET 연습(보여주기)

## 1. 클라이언트와 서버 연결 확인하기

### 서버 코드 - app.py

```python
@app.route('/memo', methods=['GET'])
def read_articles():
    return jsonify({'result':'success', 'msg':'GET 연결되었습니다!'})
```



### 클라이언트 코드 - index.html

```Javascript
$(document).ready(function () {
  showArticles();
});
function showArticles() {
  $.ajax({
    type: "GET",
    url: "/memo",
    data: {},
    success: function (response) {
      if (response["result"] == "success") {
        alert(response["msg"]);
      }
    }
  })
}
```

* **$(document).ready**에 의해, showArticles가 호출된다.
* **페이지가 새로고침되었을 때 클라이언트 코드와 서버 코드가 연결 된 것을 확인할 수 있다.**



## 2. 서버부터 만들기

* 서버 로직
  1. **mongoDB**에서 _id 값을 제외한 모든 데이터 가져오기
  2. **all_articles**라는 키 값으**로 articles 정보 보내기**



### 서버 코드 - app.py

```python
@app.route('/memo', methods=['GET'])
def listing():
    articles = list(db.articles.find({}, {'_id': False}))
    return jsonify({'all_articles':articles})
```

* **mongoDB**로부터 **ariticles 정보**를 가져온다.
* **all_articles의 키 값으로 return**



## 3. 클라이언트 만들기

* 클라이언트 로직
  1. /memo에 GET방식으로 메모 정보 요청 하고 articles로 메모 정보 받기
  2. makeCard 함수를 이용해서 카드 HTML 붙이기



### 클라이언트 코드 - index.html

```Javascript
function showArticles() {
                $.ajax({
                    type: "GET",
                    url: "/memo",
                    data: {},
                    success: function (response) {
                        let articles = response['all_articles']
                        for (let i = 0; i < articles.length; i++){
                            let title = articles[i]['title']
                            let image = articles[i]['image']
                            let url = articles[i]['url']
                            let desc = articles[i]['desc']
                            let comment = articles[i]['comment']

                            let temp_html = `<div class="card">
                                                <img class="card-img-top"
                                                     src="${image}"
                                                     alt="Card image cap">
                                                <div class="card-body">
                                                    <a target="_blank" href="${url}" class="card-title">${title}</a>
                                                    <p class="card-text">${desc}</p>
                                                    <p class="card-text comment">${comment}</p>
                                                </div>
                                            </div>`
                            $('#cards-box').append(temp_html)
                        }
                    }
                })
            }
```

* 서버로부터 **articles의 정보들을 받는다.**
* 받은 articles의 정보들을 **for문**을 통해 각각 **title, image, url, desc, comment에 접근**
* **각각 뽑아낸 정보를 html_temp에 담아 #cards-box에 append**



# Reference

**스파르타코딩 - 웹개발 종합반**