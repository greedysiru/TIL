# Understanding TypeScript(48) - Compiling Interfaces to JavaScript

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Compiling Interfaces to JavaScript

* Class의 경우 target에 따라 다른 형태로 complie
  * es6의 경우 class keyword가 유지
  * es5인 경우 생성자 함수로 compile

* interface의 경우 TypeScript Compiler가 JavaScript로 compile하며 제거
  * interface의 경우 TypeScript만의 문법이므로 JavaScript에서 대체할 수 있는 방법이 없음
  * 런타임엔 interface의 흔적이 남지 않음



### Complie Result

* TypeScript Code


```TypeScript
interface Named {
  name?: string;
}

interface Greetable extends Named {
  greet(phrase: string): void;
}

class Person implements Greetable {
  name?: string;
  
  constructor(n?: string) {
    if (n) {
      this.name = n;
    }
  }
  
  greet(phrase: string) {
    if (this.name) {
      console.log(`${phrase} ${this.name}`);
    } else {
      console.log('안녕!');
    }
  }
}

const User: Greetable = new Person();
```



* Complied Code(ES6)

```JavaScript
"use strict";
class Person {
constructor(n) {
if (n) {
this.name = n;
}
}
greet(phrase) {
if (this.name) {
console.log(`${phrase} ${this.name}`);
}
else {
console.log('안녕!');
}
}
}
const User = new Person();
```

* Complied Code(ES5)

```JavaScript
"use strict";
var Person = /** @class */ (function () {
function Person(n) {
if (n) {
this.name = n;
}
}
Person.prototype.greet = function (phrase) {
if (this.name) {
console.log("".concat(phrase, " ").concat(this.name));
}
else {
console.log('안녕!');
}
};
return Person;
}());
var User = new Person();
```

  

# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

