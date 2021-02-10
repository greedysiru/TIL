# [노마드코더]바닐라 JS로 크롬 앱 만들기 (5)(2021.1.20)



**상세 내용 [블로그](https://greedysiru.tistory.com/124) 참고**



# Make My First JS APP

## 1. Image Background

* **APP에 배경화면을 출력하는 기능**
* APP이 가지고 있는 이미지를 페이지를 들어올 때 마다 **무작위**로 보여준다.



### Math

* **JavaScript의 모듈**
* **수식에 관련된 기능을 사용**



#### Math.random()

* **난수 생성**
* **소수점이 포함**된 상태로 출력된다.
* 범위를 지정하려면 *** 숫자** 를 붙여준다.

> Math.random( ) * 5
>
> 0 ~ 5 사이의 난수 생성 (5 제외)



#### Math.floor()

* 괄호 안의 숫자의 소수를 없앤다.
* 버림 처리한다.

> Math.floor( 3.14 )
>
> 3으로 버림



#### Math.ceil()

* 괄호 안의 숫자의 소수를 없앤다.
* 올림 처리한다.

> Math.ceil( 3.14 )
>
> 4로 올림



### JavaScript

```JavaScript
const body = document.querySelector("body");

const IMG_NUMBER = 3; // images 파일에 3개의 이미지가 있음

function paintImage(imgNumber){
    const image = new Image();
    image.src = `images/${imgNumber + 1}.jpg` // 난수가 0~2까지만 생성되므로 +1 한다.
    image.classList.add('bgImage') // 생성된 이미지에 class명 bgImage를 더한다.
    body.prepend(image); // 생성된 이미지를 body에 출력한다.
    
}

function genRandom(){
    const number = Math.floor(Math.random()* IMG_NUMBER) // 3개의 이미지 만큼 난수를 생성한 뒤에 소수점은 버린다.
    return number;
}

function init(){
    const randomNumber = genRandom(); // 생성한 난수를 받아오기
    paintImage(randomNumber);  // 이미지 적용시키기
}

init();
```



### CSS

* 이미지를 불러올 때 효과를 추가

```CSS
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

.bgImage {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
  animation: fadeIn 0.5s linear;
}
```



## 2. Getting the Weather part One Geolocation

* 접속한 사용자의 **위치정보**를 가져오는 기능을 추가



### navigator API

* 위치정보를 불러올 수 있다.

>navigator.geolocation.getCurrentPosition(함수1, 함수2);
>
>함수 1: 위치 불러오기를 성공했을 때 실행
>
>함수 2: 위치 불러오기를 실패했을 때 실행



### JavaScript

```JavaScript
const COORDS = 'coords';

function saveCoords(coordsObj){
    localStorage.setItem(COORDS, JSON.stringify(coordsObj)) // 위치 정보를 local storage에 저장, 객체는 문자열 변환
}
// 위도와 경도를 가져오는 함수
function handleGeoSucces(position){ // 위치정보를 받아와서 위도와 경도 각각 저장
    const latitude = position.coords.latitude;
    const longitude = position.coords.longitude;
    const coordsObj = {
        latitude,
        longitude // 객체의 key의 이름을 같게 저장할 때는 : 뒤를 생략해도 된다.
    };
    saveCoords(coordsObj);
}
function handleGeoError(){
    console.log('Cant access geo location');
}
function askForCoords(){
    navigator.geolocation.getCurrentPosition(handleGeoSucces, handleGeoError); // 현재 위치정보를 가져와서 함수 실행
}
// api 사용 
function loadCoords(){
    const loadedCords = localStorage.getItem(COORDS);
    if(loadedCords === null){ //  local storage에 위치정보가 없을 때 실행
        askForCoords();
    } else {
        // getWeather
    }
}
function init(){
    loadCoords(); 
}
init();
```

* 아래처럼 위치 정보가 성공적으로 들어온 것을 볼 수 있다.

![스크린샷 2021-01-20 오후 8.08.06](../../../../../Desktop/스크린샷 2021-01-20 오후 8.08.06.png)



## 3. Getting the Weather part Two API

* **weather API**를 사용해서 날짜 정보를 보여준다.(https://openweathermap.org/)



### API

* **Application Programming Interface**

* **다른 서버로부터 데이터를 손쉽게 가져올 수 있는 수단**

  

### JavaScript

```JavaScript
const weather = document.querySelector(".js-weather");
const API_KEY = "ee5bad41203f8ef162df7e6c27505bd7"; // weather api key
const COORDS = 'coords';

// api로 날씨 정보 가져오기
function getWeather(lat, lon){
    fetch(`http://api.openweathermap.org/data/2.5/weatherlat=
${lat}&lon=
${lon}&appid=${API_KEY}
&units=metric`) // api로 정보를 가져온다.
    .then(function(response){
        return response.json();
    }) // 정보를 가져오고 난 후, 함수 실행
    .then(function(json){
        const temperature = json.main.temp;
        const place = json.name;
        weather.innerText = `${temperature} @ ${place}`; // 온도와 장소를 weather span에 넣는다.(출력)
        }); // 함수 실행 후 연이어 또 다른 함수 실행
}
// API를 제공하는 쪽에서 사용자가 어떤 데이터를 얼마나 가져가는지 알 수 있다.
function saveCoords(coordsObj){
    localStorage.setItem(COORDS, JSON.stringify(coordsObj))
}

function handleGeoSucces(position){
    const latitude = position.coords.latitude;
    const longitude = position.coords.longitude;
    const coordsObj = {
        latitude,
        longitude 
    };
    saveCoords(coordsObj);
    getWeather(latitued, longitude); // 위치 정보를 기반으로 weather 정보 가져오는 함수 실행
}

function handleGeoError(){
    console.log('Cant access geo location');
}

function askForCoords(){
    navigator.geolocation.getCurrentPosition(handleGeoSucces, handleGeoError); 
}

function loadCoords(){
    const loadedCords = localStorage.getItem(COORDS);
    if(loadedCords === null){
        askForCoords();
    } else {
        const parseCoords = JSON.parse(loadedCords);
        getWeather(parseCoords.latitude, parseCoords.longitude); // 사용자의 위치정보가 있는경우 날씨 정보만 불러온다.
    }
}
function init(){
    loadCoords();
}
init();
```

* **fetch** : API의 데이터를 가져온다.
* **.then** : 앞의 작업이 끝난 후 함수를 실행할 수 있다. 이 경우, API서버에서 데이터를 받아오고 난 후 함수를 실행한다. .then을 사용하지 않으면, 데이터를 온전히 전부 불러오기 전에 다음 함수를 실행하므로 정상적으로 작동하지 않을 수 있다.



# Reference

https://nomadcoders.co/javascript-for-beginners/lobby