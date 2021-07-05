# [드림코딩 by 엘리] JavaScript 기초 강의(10) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/566) 참고**



# callback

* 나중에 다시 불릴 전달되는 함수
* arrow function으로 간단하게 전달

## 1. 동기와 비동기

### 동기

> **JavaScript is synchronous.**

* 자바스크립트는 동기적이다.
* hoisting된 이후부터 코드가 순서에 맞춰 동기적으로 실행된다.
  * hoisting: var, function decalaration이 자동으로 제일 위로 올라감



### 비동기

* 언제 코드가 실행될 지 예측할 수 없는 것

* setTimeout: web API

  * 브라우저에서 제공
  * 지정된 시간이 지나면 callback 함수를 실행

  ```JavaScript
  console.log('1');
  setTimeout(() => console.log('2'), 1000 );
  console.log('3');
  // 1 3 2의 순서로 출력됨
  ```

  setTimeout이 실행되고 1초가 경과될 때까지 기다리지 않고 아래줄을 실행한다.



## 2. callback 정리

### Synchronous callback

```JavaScript
console.log('1');
setTimeout(() => console.log('2'), 1000 );
console.log('3');

function printImmediately(print){
  print();
}
printImmediately(() => console.log('hello'));
// 1 3 hello 2 출력
```

**실제 코드 실행은 아래와 같다.**

```JavaScript
// hoisting
function printImmediately(print){
  print();
}

console.log('1');
setTimeout(() => console.log('2'), 1000 );
console.log('3');

printImmediately(() => console.log('hello'));
```



### Asynchronous callback

```JavaScript
function printWithDelay(print, timeout){
  setTimeout(print, timeout);
}
printWithDelay(() => console.log('async callback'), 2000);
```



## 3. callback 지옥 체험

```JavaScript
class UserStorage {
  loginUser(id, password, onSuccess, onError) {
    setTimeout(() => {
      if (
        (id === 'siru' && password === 'greedy') ||
        (id === 'jm' && password === 'jeon')
      ) {
        onSuccess(id);
      } else {
        onError(new Error('not found'));
      }
    }, 2000);
  }
  getRoles(user, onSuccess, onError) {
    setTimeout(() => {
      if (user === 'jm') {
        onSuccess({ name: 'jm', role: 'admin' });
      } else {
        onError(new Error('no access'));
      }
    }, 1000);
  }
}

const userStorage = new UserStorage();
const id = prompt('enter your id');
const password = prompt('enter toru password');
userStorage.loginUser(
  id,
  password,
  user => {
    userStorage.getRoles(user,
      userWithRole => {
        alert(`Hello ${userWithRole.name}, you have a ${userWithRole.role}`);
      },
      error => {
        console.log(error);
      }
    )
  },
  error => { console.log(error) }
);
```



## 4. callback chain의 문제점

* 가독성이 좋지 않다.
  * 비지니스 로직을 파악하기 어렵다.
* 디버깅, 에러 처리가 어렵다.
* 유지보수가 어렵다



# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)