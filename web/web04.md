# [스파르타코딩] 웹개발 종합반 항해 1기 2주차 (2)(2021.2.2 ~3)



**상세 내용 [블로그](https://greedysiru.tistory.com/159) 참고**

# 1. 서버 - 클라이언트 통신 이해하기

## 서버 -> 클라이언트

* **JSON** :**서버가 클라이언트에게 주는 데이터의 포맷**
  * **key : value**로 이루어져 있다.



## 클라이언트 -> 서버

* **API** : 은행창구와 같은것
* **GET** : 통상적으로 **데이터 조회(Read)**를 요청할 때
* **POST** : 통상적으로 **생성(Create), 변경(Update), 삭제(Delete)** 요청할 때



### GET

* **?** : 여기서부터 전달할 데이터가 작성된다는 의미
* **&** : 전달할 데이터가 더 있다는 뜻
* 어떤 요청을 받았을 때, 어떤 정보를 주는지는 프론트엔드 개발자와 백엔드 개발자가 미리 정한 **약속**이다.

> google.com/search?q=아이폰&sourceid=chrome&ie=UTF-8
>
> q = 아이폰 (**검색어**)
>
> sourced=chrome (**브라우저 정보**)
>
> ie=UTF-8 (**인코딩 정보)**



# 2. Ajax 시작하기

* Ajax는 JQuery를 임포트한 페이지에서만 동작 가능하다.



## Ajax 코드

```javascript
$.ajax({
  type: "GET", // GET 방식으로 요청
  url: "",  // API
  data: {}, // POST 방식에서 사용
  success: function(response){ // 서버에서 준 결과를 response라는 변수에 담음
    console.log(response) // 서버에서 준 결과를 이용해서 나머지 코드를 작성
  }
})
```

* **type**: "GET"
  * GET 방식으로 요청
* **url**: 요청할 url, 보통 API
* **data**: 요청하면서 함께 줄 데이터
* **success**: 성공시, **response** 값에 서버의 결과 값을 담아 함수 실행



# 3. Ajax 함께 연습하기

## 미세먼지 Open API

* 실시간 미세먼지를 화면에 출력한다.
* 미세먼지 지수가 60인 경우, 폰트 **color =red** 적용한다.

```HTML
<!doctype html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <title>jQuery 연습하고 가기!</title>

    <!-- jQuery import -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>

    <style type="text/css">
        div.question-box {
            margin: 10px 0 20px 0;
        }
        .bad {
            color: red; /* 미세먼지 나쁨인 경우의 폰트색상 red */
            font-weight: bold;
        }
    </style>

    <script>
        function q1() {
            $('#names-q1').empty(); // 리스트 중복을 방지하기 위해 전부 비워준다.
            $.ajax({
                type: "GET",
                url: "http://openapi.seoul.go.kr:8088/6d4d776b466c656533356a4b4b5872/json/RealtimeCityAir/1/99", // 미세먼지 API
                data: {},
                success: function (response) {
                    let rows = response["RealtimeCityAir"]["row"]; // 도시별 미세먼지 지수 추출
                    for (let i = 0; i < rows.length; i++) { // for문으로 모든 요소 접근
                        let gu_name = rows[i]['MSRSTE_NM']; // 도시명
                        let gu_mise = rows[i]['IDEX_MVL'];  // 미세먼지 지수

                        let temp_html = ''

                        if (gu_mise > 60) {
                            temp_html = `<li class="bad">${gu_name} : ${gu_mise}</li>` // 60보다 심할 경우
                        } else {
                            temp_html = `<li>${gu_name} : ${gu_mise}</li>`
                        }
                        
                        $('#names-q1').append(temp_html);
                    }
                }
            })
        }
    </script>

</head>

<body>
    <h1>jQuery+Ajax의 조합을 연습하자!</h1>

    <hr />

    <div class="question-box">
        <h2>1. 서울시 OpenAPI(실시간 미세먼지 상태)를 이용하기</h2>
        <p>모든 구의 미세먼지를 표기해주세요</p>
        <p>업데이트 버튼을 누를 때마다 지웠다 새로 씌여져야 합니다.</p>
        <button onclick="q1()">업데이트</button> <!-- 버튼을 누르면, 함수 실행 -->
        <ul id="names-q1">
        </ul>
    </div>
</body>

</html>
```

* 미세먼지 지수가 60 초과한 경우, **if문에 의해서, class = bad인 리스트가 생성된다.**
  * 그렇지 않은 경우, 해당 클래스 없이 생성
* **class = bad**는 css로 폰트 **color = red를 적용**하였다.

## JQuery 이미지  src 변경

> $('#img').attr('src',imgurl);

* 첫 번째 인자에 **src**, 두 번째 인자에 **img의 url**을 넣는다.

# Refernce

**스파르타코딩 - 웹개발 종합반**