# TypeScript(6)

**본 내용은 Nomad Coders - TypeScript로 블록체인 만들기 강의를 토대로 작성하였습니다.**



## 1. readonly

* property에 읽기 전용 속성 부여
* public property이어도 내용을 수정할 수 없음
* TypeScript keyword



## 2. static

* JavaScript keyword
* 인스턴스 메서드가 아닌, 클래스 생성자 자체에 정의된 메서드
* 클래스를 생성하지 않아도 사용할 수 있음



## 3. interface

* typer과의 차이
  * object의 형태만을 정의
  * type은 다양한 목적으로 사용 가능
* 상속(extends)의 대상이 될 수 있음
  * type의 경우에는 &(and)으로 표현
* 객체지향 프로그래밍과 유사한 문법
  * 클래스의 모양도 정의 가능
* 같은 interface를 여러번 선언하면, 합쳐짐

```TypeScript
interface Cat {
  name: string;
  gender: 'female' | 'male';
}

interface Siru extends Cat {}

const siru: Siru = {
  name: 'siru',
  gender: 'female',
}

---------------------------------------------
      
type Cat = {
  name: string;
  gender: 'female' | 'male';
}

type Siru = Cat & {}

const siru: Siru = {
  name: 'siru',
  gender: 'female',
}
```



## 4. 추상 클래스와 interface

* 추상 클래스는 인스턴스를 만들 수 없고 다른 클래스에 상속을 시킬 목적으로 정의
* 추상 클래스는 JavaScript에는 존재하지 않는 개념으로 JavaScript로 컴파일 될 때는 결국 클래스로 변함
  * 트리세이킹이 적용되지 않음
* interface로 추상 클래스를 대체가능 
  * 클래스의 모양을 특정지을 수 있음
  * implements라는 TypeScript로 해당 interface를 기반으로 클래스 구현
  * 트리세이킹이 적용되어 컴파일 후에 JavaScript에서는 제거가 됨
  * 가벼운 코드
* interface를 implements를 할 때는 property가 public이어야 함
* implements 키워드는 콤마를 기준으로 여러개의 interface를 구현토록 Class에 지정할 수 있음

```TypeScript
interface Pet {
  name: string;
  gender: 'male' | 'female'
  cry(): string;
  introduce(): string;
}

class Cat implements Pet {
  constructor(
	  public name: string,
    public gender: string
  ){}
  
  cry(){
    console.log('야옹');
  }
  
  introduce(){
    console.log(`안녕, 난 ${this.name}이야`);
  }
}
```



# Reference

[Nomad Coders - TypeScript로 블록체인 만들기](https://nomadcoders.co/typescript-for-beginners/lobby)

