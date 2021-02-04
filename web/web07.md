# [스파르타코딩] 웹개발 종합반 항해 1기 4주차 (1)(2021.2.4)



**상세 내용 [블로그](https://greedysiru.tistory.com/164?category=875936) 참고**



# 1. Flask 시작하기

* Flask: 파이썬의 웹 프레임워크
  * 서버를 구동시켜주는 편한 코드 모음
  * 복잡한 일을 쉽게 할 수 있다.



## Flask 시작 코드

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
   return 'This is Home!'

if __name__ == '__main__':  
   app.run('0.0.0.0',port=5000,debug=True)
```

* 코드를 실행하면, http://localhost:5000/으로 접속할 수 있다.



## URL 나눠보기

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
   return 'This is Home!'

@app.route('/mypage') # /mypage url
def mypage():  
   return 'This is My Page!'

if __name__ == '__main__':  
   app.run('0.0.0.0',port=5000,debug=True)
```

* **@app.route('/')** 부분을 수정해서 URL을 나눌 수 있다.
* **url 별로 함수명이 같거나, route('/')내의 주소가 같으면 안된다.**



# 2. Flask 시작하기 - HTML 파일 주기

## Flask의 기본 폴더구조

* 프로젝트 폴더 안에 **항상 아래처럼 세팅**한다.
  * **static 폴더**: 이미지, css파일을 넣는다.
  * **templates 폴더**: html 파일을 넣는다.
  * **app.py 파일**



## HTML 파일 불러오기

* **templates** 폴더에서 **HTML을 파일**을 불러온다.
* flask 내장함수 **render_template**를 이용

```python
from flask import Flask, render_template
app = Flask(__name__)

@app.route('/')
def home():
   return render_template('index.html') # templates폴더에서 index.html을 가져와 화면에 출력

if __name__ == '__main__':
   app.run('0.0.0.0', port=5000, debug=True)
```



# 3. Flask 시작하기 - 본격 API 만들기

## GET, POST 방식

* GET
  * **데이터 조회(Read)**를 요청할 때
  * **데이터 전달**: URL 뒤에 물음표를 붙여 key=value로 전달
  * 예: google.com?q=북극곰
* POST
  * **생성(Create), 변경(Update), 삭제(Delete)** 요청할 때
  * **데이터 전달**: 바로 보이지 않는 HTML body에 key:value 형태로 전달



## GET 요청에서 클라이언트 데이터 받기

### GET 요청 API 코드

```python
@app.route('/test', methods=['GET']) # GET 방식
def test_get():
   title_receive = request.args.get('title_give')
   print(title_receive)
   return jsonify({'result':'success', 'msg': '이 요청은 GET!'})
```

* **title_give**로 받은 값을 print로 출력하게 된다.
  * 봄날을 간다 출력
* **return**으로 **{'result':'success', 'msg': '이 요청은 GET!'}**

### GET 요청 확인 Ajax 코드

```Javascript
$.ajax({
    type: "GET",
    url: "/test?title_give=봄날은간다", // url로 입력
    data: {},
    success: function(response){
       console.log(response)
    }
  })
```

* **titlte_give=봄날은간다** 를 보낸다.
* **response**로 **{msg: "이 요청은 GET!", result: "success"}** 을 받는다.
  * 콘솔에서 출력된다.

## POST 요청에서 클라이언트 데이터 받기

### POST 요청 API 코드

```python
@app.route('/test', methods=['POST'])
def test_post():
   title_receive = request.form['title_give']
   print(title_receive)
   return jsonify({'result':'success', 'msg': '이 요청은 POST!'})
```

* **title_give**로 받은 값을 print로 출력하게 된다.
  * 봄날은간다 출력
* **return**으로 **{'result':'success', 'msg': '이 요청은 POST!'}**

### POST 요청 확인 Ajax 코드

```Javascript
$.ajax({
    type: "POST",
    url: "/test",
    data: { title_give:'봄날은간다' }, // data로 입력
    success: function(response){
       console.log(response)
    }
  })
```

* **titlte_give=봄날은간다** 를 보낸다.
* **response**로 **{msg: "이 요청은 POST!", result: "success"}** 을 받는다.
  * 콘솔에서 출력된다.





# Reference

**스파르타코딩 - 웹개발 종합반**