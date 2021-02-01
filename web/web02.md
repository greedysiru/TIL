

# [스파르타코딩] 웹개발 종합반 항해 1기 1주차 (2)(2021.2.2)



**상세 내용 [블로그](https://greedysiru.tistory.com/156) 참고**



# 1. Javascript 맛보기

* Javascript
  * **브라우저가 알아들을 수 있는 프로그래밍 언어**
  * 웹 페이지를 **움직이게 한다.**
  * 역사적으로 이미 만들어진 표준이기 때문에 **모든 브라우저는 Javascript를 이해한다.**

## HTML과 연결

* **head 태그**에 **script 태그**를 작성한다
* 함수를 정의하여 웹 페이지에 기능을 추가할 수 있다.
* 예시

```HTML
<head>
      <script>
        function hey(){ // 함수 정의
            alert('안녕!');
        }
    </script>
</head>
<body>
  <p class="lead">
    <a onclick="hey()" role="button">포스팅박스 열기</a> <!-- 클릭시 함수 호출 -->
  </p>
</body>
```



# 2. Javascript 기초 문법 (1)

## 변수 & 기본연산

> let 변수명 = 값

* 오른쪽에 있는 값을 왼쪽의 변수에 넣는다.
* **let**으로 선언
* **사칙연산, 문자열 더하기**가 가능하다.
* 변수명 정하는 규칙: 회사마다 다르며, 크게 아래의 두 가지가 있다.
  * **snake case**
  * **camel case**

> **snake case** first_name = 'bob'
>
> **camel case** firstName = 'bob'



## 리스트 & 딕셔너리

### 리스트

* 순서를 가지는 데이터 묶음
* 선언과 접근 예시

```Javascript
let a_list = [] // 대괄호로 표현

let b_list = [1, 2, 'hey', 3] // 값을 넣은 채로 초기화

b_list[1] // 1번 인덱스인 2 출력
b_list[2] // 'hey'를 출력

// 리스트에 요소 넣기
b_list.push('헤이') // 리스트 끝에 값을 넣고 리스트의 길이를 return

// 리스트의 길이 구하기
b_list.length // 5 출력
```



### 딕셔너리

* 키(key) - 밸류(value) 값의 묶음
* 선언과 접근 예시

```Javascript
let a_dict = {} // 중괄호로 표현

let b_dict = {'name' : 'Bob', 'age' : 21} // 값을 넣은 채로 초기화

b_dict['name'] // 'Bob'을 출력
b_dict['age']  // 21을 출력

b_dict['height'] = 180 // 딕셔너리에 키 : 밸류 넣기
```



### 리스트와 딕셔너리의 조합

* 순서를 표시하고 정보를 묶을 수 있도록 할 수 있다.

```Javascript
names = [{'name':'bob','age':20},{'name':'carry','age':38}]

// names[0]['name']의 값은? 'bob'
// names[1]['name']의 값은? 'carry'

new_name = {'name':'john','age':7}
names.push(new_name)

// names의 값은? [{'name':'bob','age':20},{'name':'carry','age':38},{'name':'john','age':7}]
// names[2]['name']의 값은? 'john'
```



## 기본 함수

* **%** : 나눗셈의 나머지
* **.toUpperCase()** :알파벳을 대문자로 변환
* **.split()** : 특정 문자로 문자열을 나누기

```Javascript
let myemail = 'sparta@gmail.com'
myemail.split('@')[1].split('.')[0] // gmail 
```

<br>

* **.join()** : 특정 문자로 합치기

```Javascript
let txt = '서울시-마포구-망원동'
let names = txt.split('-'); // ['서울시','마포구','망원동']
let result = names.join('>');  // '서울시>마포구>망원동'
```



# 3. Javascript 기초 문법 (2)

## 함수

* 기본 생김새

> function 함수이름(필요 변수들) {
>
> ​        내릴 명령
>
> }

* 호출

> 함수이름(필요 변수들);



## 조건문

* **조건에 맞는 경우 명령어를 실행**
* 예시

```Javascript
// AND
function is_adult(age, sex){ // 2개의 변수를 받는 함수
	if(age > 20 && sex == '여'){ // 나이가 20세이고 성별이 여자인 경우
		alert('성인 여성')           // 경고창에 성인 여성 출력
	} else if (age > 20 && sex == '남') {
		alert('성인 남성')
	} else {
		alert('청소년이에요')
	}
}

// OR
function is_adult(age, sex){
	if (age > 65 || age < 10) { // 나이가 65세 초과 또는 10살보다 어린 경우
		alert('탑승하실 수 없습니다')  // 탑승불가 메시지 경고창 출력
	} else if(age > 20 && sex == '여'){
		alert('성인 여성')
	} else if (age > 20 && sex == '남') {
		alert('성인 남성')
	} else {
		alert('청소년이에요')
	}
}
```



## 반복문

* **반복된 작업을 실행할 때 사용한다.**
* 기본 생김새

> for( 1. 시작조건; 2. 반복조건; 3. 더하기) {
>
> ​        4. 매번실행
>
> }



### 반복문 - 리스트, 딕셔너리 호출

* 아래와 같이 리스트, 딕셔너리에 하나하나 접근하거나 조건에 맞게 접근할 수 있다.

```Javascript
let scores = [
	{'name':'철수', 'score':90},
	{'name':'영희', 'score':85},
	{'name':'민수', 'score':70},
  {'name':'형준', 'score':50},
  {'name':'기남', 'score':68},
  {'name':'동희', 'score':30},
]

for (let i = 0 ; i < scores.length ; i++) {       // 리스트 내의 딕셔너리 하나씩 출력
	console.log(scores[i]);
}

for (let i = 0 ; i < scores.length ; i++) {       // 점수가 70점 미만인 사람들의 이름 출력
	if (scores[i]['score'] < 70) {
		console.log(scores[i]['name']);
	}
}
```



# Reference

**스파르타코딩 - 웹개발 종합반**

