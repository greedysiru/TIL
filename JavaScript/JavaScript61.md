# JavaScript - Callback, Promise

**본 내용은 인프런 장기효(캡틴판교)님의 Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념 강의를 토대로 작성하였습니다.**



## 1.Callback

* 특정 함수나 기능이 종료되는 시점에 실행되는 함수
  * JavaScript는 인자에 함수를 넘기를 수 있음



### ajax

* jQuery에서 데이터 요청할 때 사용하는 내장 api
* 데이터 요청 성공 시에 Callback 함수 실행
* JavaScript의 특성상 데이터 요청의 응답을 기다리지 않음
  * 비동기 처리를 해야 함
  * Callback으로 처리할 수 있음
  * Callback Hell: Callback이 중첩되면서 코드가 가독성이 떨어지고 복잡해짐
  * 사고의 위배: 사람의 사고에 위배되는 코드

```JavaScript
function fetchData() {
  var result = [];
  
  $.ajax({
		url: 'url',
		// Callback
    success:function(data) {
    console.log('데이터 호출 결과', data);
    result = data;
    console.log('함수 결과', result);
    
    // 비동기 처리를 위한 Callback
    getResult(function() {
      parseResult(function() {
        ...
      })
    })
      
  	}
	});
}

fetchData();
```



## 2. Promise

* 비동기 처리 패턴
* Callback의 문제점을 극복
* 직관적인 코드
* Promise는 호출 시에 resolve와 reject를 인자로 받음
  * resolve 성공한 경우의 처리
  * reject 실패한 경우의 처리
* Promise 객체를 받은 뒤에 then, catch 사용 가능
  * then 성공한 경우(resolve와 연결)
  * catch 실패한 경우(reject와 연결)
* Promise Chaining

```JavaScript
function callAjax() {
  // Promise 객체 return
  return new Promise(function (resolve, reject) {
    $.ajax({
      url: 'url',
      success:function(data) {
        resolve(data);
      }
    });
  });
}

function fetchData() {
  var result = [];
  
  callAjax()
  	.then(function(data) {
    	console.log('데이터 호출 결과', data);
    	result = data;
    	console.log('함수 결과', result);
  	});
}
```



# Reference

[Vue.js 완벽 가이드 - 실습과 리팩토링으로 배우는 실전 개념](https://www.inflearn.com/course/vue-js/dashboard)

