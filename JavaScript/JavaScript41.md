# [드림코딩 by 엘리] JavaScript 기초 강의(11) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/567) 참고**



# Promise

* JavaScript에서 제공되는 비동기를 간단하게 처리할 수 있는 Object
* 콜백함수 대신 사용할 수 있다.
* Promise 안에서는 무거운 일을 수행하게 된다.
  * 네트워크에서 데이터를 받아오거나 파일에서 큰 데이터를 읽는 과정을 수행하는 것을 동기적으로 처리하면, 다음 코드가 실행되지 않으므로 비동기 처리를 하는 것이 좋다.
* state
  * 상태
  * process가 동작을 수행중인지, 완료되어서 성공 또는 실패했는지
* producer / consumer
  * 정보 제공자 / 소비자



## 1. state

> **pending -> fulfilled or rejected**

* pending: operation을 수행 중
* fulfilled: operation을 완료하고 성공
* rejected: operation을 완료했지만 실패 



## 2. Producer

* `new`키워드로 `Promise()`객체 생성
* `executor` : Promise의 생성자인 콜백함수, 하위에 두개의 콜백함수를 가지고 있다.
  * `resolve`: 기능이 정상적으로 수행되었을 때 데이터를 전달하는 콜백함수
  * `reject`: 기능을 수행하다가 문제 발생시 호출되는 콜백함수
* `Promise`를 만드는 순간 `executor`가 바로 실행
  * 네트워크 통신코드를 넣어 놓았다면, `Promise`가 만들어지는 순간 통신을 수행
  * 불필요한 통신을 할 수 있으므로 주의

```JavaScript
const promise = new Promise((resolve, reject) => {
  // doing some heavy work(network, read files)
  console.log('doing something...');
  setTimeout(() => {
    resolve('siru');
  }, 2000);
});
```



## 3. Consumers

* `then, catch, finally`를 이용해서 값을 받아올 수 있다.
  * chaining을 할 수 있다.



### then

* promise가 정상적으로 잘 수행이되었을 때
* 값을 전달하거나 promise를 전달
* 같은 promise를 return

```JavaScript
const promise = new Promise((resolve, reject) => {
  // doing some heavy work(network, read files)
  console.log('doing something...');
  setTimeout(() => {
    resolve('siru');
  }, 2000);
});

promise.then((value) => {
  console.log(value);
});
```



### catch

* promise가 수행중에 Error 발생했을 때
  * `Error`: JavaScript에서 제공하는 obejct 

```JavaScript
const promise = new Promise((resolve, reject) => {
  // doing some heavy work(network, read files)
  console.log('doing something...');
  setTimeout(() => {
    reject(new Error('no network'));
  }, 2000);
});

promise.then((value) => {
  console.log(value);
})
.cath(error => {
  consoel.log(error);
});
```



### finally

*  성공, 실패와 관계없이 무조건 마지막에 호출

```JavaScript
const promise = new Promise((resolve, reject) => {
  // doing some heavy work(network, read files)
  console.log('doing something...');
  setTimeout(() => {
    reject(new Error('no network'));
  }, 2000);
});

promise.then((value) => {
  console.log(value);
})
.cath(error => {
  consoel.log(error);
}),finally(() => {
  console.log('finally');
});
```



## 4. Promise chaining

```JavaScript
const fetchNumber = new Promise((resolve, reject) => {
  setTimeout(() => resolve(1), 1000);
});

fetchNumber
.then(num => num * 2)
.then(num -> num * 3)
.then(num => {
  return new Promise((resolve, reject) => {
    setTimeout((() => resolve(num - 1), 1000))
  });
})
.then(num => console.log(num));
```



## 5. 오류 처리

```JavaScript
const getHen = () =>
	new Promise((resolve, reject) => {
    setTimeout(() => resolve('🐓'), 1000);
  });
const getEgg = hen =>
	new Promise((resolve, reject) => {
    setTimeout(() => reject(new Error(`error! ${hen} => 🥚`)), 1000);
  });
const cook = egg =>
	new Promise((resolve, reject) => {
    setTimeout(() => resolve(`${egg} => 🍳`), 1000);
  });

// getEgg에서 오류가 발생해도 적절한 처리를 할 수 있다.
getHen()
	.then(getEgg)
	.catch(error => {
  return '🥖';
	})
	.then(cook)
	.then(console.log)
	.catch(console.log);
```



## 6. 콜백함수 개선

```JavaScript
class UserStorage {
  loginUser(id, password) {
    return new Promise((resolve, reject) => {
            setTimeout(() => {
        if (
          (id === 'siru' && password === 'greedy') ||
          (id === 'jm' && password === 'jeon')
        ) {
          resolve(id);
        } else {
          reject(new Error('not found'));
        }
      }, 2000);
    });
  }
  
  
  getRoles(user) {
    return new Promise((resolve, reject) => {
            setTimeout(() => {
        if (user === 'jm') {
          resolve({ name: 'jm', role: 'admin' });
        } else {
          reject(new Error('no access'));
        }
      }, 1000);
    });
  }
}

const userStorage = new UserStorage();
const id = prompt('enter your id');
const password = prompt('enter toru password');
userStorage.loginUser(id, password)
.then(userStorage.getRoles)
.then(user => alert( `Hello ${user.name}, you have a ${user.role}`))
.catch(console.log);
```



# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)
