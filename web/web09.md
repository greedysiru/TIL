# [스파르타코딩] 웹개발 종합반 항해 1기 5주차 (1)(2021.2.5)



**상세 내용 [블로그](https://greedysiru.tistory.com/167) 참고**

# 무비스타

# 1. GET연습(보여주기)

* DB로부터 영화배우 정보를 가져와서 보여준다.
* 필요한 데이터
  * 영화배우 이름
  * 영화배우 이미지 : 이미지 src 속성
  * 좋아요 개수
  * 최근 작품 내용이 들어가는 부분



## 1. 클라이언트와 서버 연결 확인하기

* **/api/list , GET**

### 서버 코드 - app.py

```python
@app.route('/api/list', methods=['GET'])
def show_stars():
    sample_receive = request.args.get('sample_give')
    print(sample_receive)
    return jsonify({'msg': 'list 연결되었습니다!'})
```

### 클라이언트 코드 - index.html

```javascript
function showStar() {
      $.ajax({
          type: 'GET',
          url: '/api/list?sample_give=샘플데이터',
          data: {},
          success: function (response) {
              alert(response['msg']);
          }
      });
  }
```



## 2. 서버부터 만들기

* DB의 영화배우 정보들을 ID제외 후 가져온다.
* **like가 많은 순으로 정렬**한다.
* 성공하면 succes 메시지와 함께 stars_list 목록을 클라이언트에 전달

```python
@app.route('/api/list', methods=['GET'])
def show_stars():
    movie_star = list(db.mystar.find({}, {'_id': False}).sort('like', -1))
    return jsonify({'movie_stars': movie_star})
```

* **find 뒤에 .sort 메소드를 사용한다,**
  * **like를 기준으로 내림차순(-1) 정렬**



## 3. 클라이언트 만들기

* 클라이언트 로직
  * **GET 방식**으로 **/api/list 주소**로 **star_list 요청**
  * 서버가 돌려준 **satrs_list**를 **stars라는 변수에 저장**
  * **for문**으로 stars 배열의 요소 차례대로 조회
  * 영화배우 카드 코드를 **#star-box**에 붙이기

```Javascript
function showStar() {
                $.ajax({
                    type: 'GET',
                    url: '/api/list?sample_give=샘플데이터',
                    data: {},
                    success: function (response) {
                        let mystars = response['movie_stars']
                        console.log(mystars)
                        for (let i = 0; i < mystars.length; i++){
                            let name = mystars[i]['name']
                            let img_url = mystars[i]['img_url']
                            let recent = mystars[i]['recent']
                            let url = mystars[i]['url']
                            let like = mystars[i]['like']

                            let temp_html = `<div class="card">
                                                <div class="card-content">
                                                    <div class="media">
                                                        <div class="media-left">
                                                            <figure class="image is-48x48">
                                                                <img
                                                                        src="${img_url}"
                                                                        alt="Placeholder image"
                                                                />
                                                            </figure>
                                                        </div>
                                                        <div class="media-content">
                                                            <a href="${url}" target="_blank" class="star-name title is-4">${name} (좋아요: ${like})</a>
                                                            <p class="subtitle is-6">${recent}</p>
                                                        </div>
                                                    </div>
                                                </div>
                                                <footer class="card-footer">
                                                    <a href="#" onclick="likeStar('${name}')" class="card-footer-item has-text-info">
                                                        위로!
                                                        <span class="icon">
                                              <i class="fas fa-thumbs-up"></i>
                                            </span>
                                                    </a>
                                                    <a href="#" onclick="deleteStar('김다미')" class="card-footer-item has-text-danger">
                                                        삭제
                                                        <span class="icon">
                                              <i class="fas fa-ban"></i>
                                            </span>
                                                    </a>
                                                </footer>
                                            </div>`
                            $('#star-box').append(temp_html)
                        }
                    }
                });
            }
```



# 2. POST연습(좋아요 기능)

* 클라이언트에서 받은 이름(name_give)으로 찾아서 좋아요(like)를 증가

## 1. 클라이언트와 서버 연결 확인하기

* **/api/lie , POST**

### 서버 코드 - app.py

```python
@app.route('/api/like', methods=['POST'])
def like_star():
    sample_receive = request.form['sample_give']
    print(sample_receive)
    return jsonify({'msg': 'like 연결되었습니다!'})
```



### 클라이언트 코드 - index.html

```Javascript
function likeStar(name) {
    $.ajax({
        type: 'POST',
        url: '/api/like',
        data: {sample_give:'샘플데이터'},
        success: function (response) {
            alert(response['msg']);
        }
    });
}
```



## 2. 서버부터 만들기

```python
@app.route('/api/like', methods=['POST'])
def like_star():
    name_receive = request.form['name_give']

    target_star = db.mystar.find_one({'name': name_receive})
    current_like = target_star['like']

    new_like = current_like + 1
    db.mystar.update_one({'name': name_receive}, {'$set': {'like': new_like}})

    return jsonify({'msg': '좋아요 완료!'})
```

* 좋아요 수를 올릴 영화배우의 이름 **name_give**를 받아온다.
* DB에서 **해당 이름의 영화배우 정보를 찾는다.**
* 1을 더하고 **다시 DB에 저장한다.**



## 3. 클라이언트 만들기

```Javascript
function likeStar(name) {
  $.ajax({
    type: 'POST',
    url: '/api/like',
    data: {name_give:name},
    success: function (response) {
      alert(response['msg']);
      window.location.reload()
    }
  });
}
```

* **html 문서에서 likeStar 함수가 호출 되면 API 호출**
* 영화 배우의 이름이 전달 되면, **API로 부터 response**를 받아 **경고 문구 출력 후 화면이 새로고침**된다.



# 3. POST연습(삭제하기)

* 삭제 버튼을 누르면 해당 배우의 카드가 삭제되도록 한다.
* **클라이언트와 서버 연결 확인 -> 서버 만들기 -> 클라이언트 만들기** 순으로 진행

## 완성 코드

### 서버 코드 - app.py

```python
@app.route('/api/delete', methods=['POST'])
def delete_star():
    name_receive = request.form['name_give']
    db.mystar.delete_one({'name': name_receive})
    return jsonify({'msg': '삭제 완료!'})
```

* **클라이언트로부터 받은 삭제할 영화배우의 정보를 삭제한다.**



### 클라이언트 코드 - index.html

```Javascript
function deleteStar(name) {
  $.ajax({
    type: 'POST',
    url: '/api/delete',
    data: {name_give: name},
    success: function (response) {
      alert(response['msg']);
      window.location.reload();
    }
  });
}
```

* **삭제할 배우의 이름을 서버로 보낸다**
* 그 이후 서버로부터 응답을 받으면 페이지 새로고침



# Reference

**스파르타코딩 - 웹개발 종합반**