# Understanding TypeScript(47) - Optional Parameters & Properties

**본 내용은 Udemy의 Understanding TypeScript 강의를 토대로 작성하였습니다.**



## Optional Parameters & Properties

* interface와 class에도 선택적인 속성을 정의할 수 있음
* 선택적(optional)의 의미로 ?를 붙임

```TypeScript
// 이 인터페이스를 구현하는 클래스에서 선택적으로 name 정의
interface Named {
  name?: string;
}

interface Greetable extends Named {
  greet(phrase: string): void;
}

// 마찬가지로 클래스에서도 선택적으로 name 정의 가능
class Person implements Greetable {
  name?: string;
  
  // 선택적 매개변수를 적용
  constructor(n?: string) {
    if (n) {
      this.name = n;
    }
  }
  
  // 선택적 속성이 있느냐에 따라서 메서드의 로직 처리
  greet(phrase: string) {
    if (this.name) {
      console.log(`${phrase} ${this.name}`);
    } else {
      console.log('안녕!');
    }
  }
}

// 새 인스턴스를 생성 시 파라미터를 넘기지 않아도 됨
const User: Greetable = new Person();
```



# Reference

[[Udemy] Understanding Typescript](https://www.udemy.com/course/understanding-typescript/)

