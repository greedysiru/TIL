# console

**본 내용은 드림코딩 by 엘리님의 콘솔 로그 제대로 쓰고 있을까? 강의를 토대로 작성하였습니다.**



## console

* 중요도나 심각성에 따라서 메소드가 있음



### 1. console.log

* 데이터를 출력
* 배열 형태로 여러가지 출력 가능
* 배포시에는 삭제
  * 성능에 영향

```JavaScript
console.log('log');
```



### 2. console.info

* 특정한 정보를 출력
* 배포시에는 삭제

```JavaScript
console.info('info');
```



### 3. console.warn

* 경보단계에서 출력

```JavaScript
console.warn('warn');
```



### 4. console.error

* 에러일 때 출력
* 예상하지 못한 에러, 시스템 에러

```JavaScript
console.error('error');
```



### 5. console.assert

* 거짓일 때만 출력하도록 할 수 있음

```JavaScript
console.assert(2 === 3, 'not same'); // not same 출력
console.assert(2 === 2, 'same'); // 출력되지 않음
```



### 6. console.table

* 가독성이 좋은 형태로 object 출력

```JavaScript
console.table(obj);
```



### 7. console.dir

* 깊이있게 중첩된 object를 출력
* option 전달 가능
  * depth: object의 depth 지정

```JavaScript
console.dir(obj, { colors: false, depth: 1 })
```



### 8. console.time, console.timeEnd

* console.time이 호출된 시점으로부터 console.timeEnd가 호출된 시점까지의 걸린 시간을 알 수 있음

```JavaScript
console.time('for loop');
for (let i = 0; i < 10; i++) {
  i ++;
}
console.timeEnd('for loop');
```



### 9. console.count, console.countReset

* console.count: 특정 함수가 몇 번 호출되었는지 출력
* console.countReset: 카운트 초기화

```JavaScript
function a() {
  console.count('a function');
}
a(); // a function: 1
a(); // a function: 2
a(); // a function: 3
```



## 10. console.trace

* 함수가 어디에서 호출되었는지 알 수 있음
  * 어떤 함수가 어떤 파일에서 몇 번째 줄에서 호출 했는 지 알 수 있음

```JavaScript
function f1() {
  f2();
}

function f2() {
  f3();
}

function f3() {
  console.trace();
}

f1();
```





## console.log, console.info Vs. console.warn, console.error

* console.log, console.info의 경우 배포시에 출력이 되지 않도록 설정할 수 있음
* console.warn, console.error 경우 특별한 동작을 하도록 설정할 수 있음

# Reference

[[드림코딩 by 엘리]콘솔로그 제대로 쓰고 있을까?](https://www.youtube.com/watch?v=KxsVV5jbJe4)

