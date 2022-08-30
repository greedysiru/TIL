# TypeScript(7)

**본 내용은 Nomad Coders - TypeScript로 블록체인 만들기 강의를 토대로 작성하였습니다.**



## 다형성을 활용한 클래스 정의 예시

* 다형성이란, 다양한 형태를 가질 수 있도록 하는 것
  * 제네릭을 활용

```TypeScript
// 제네릭이 지정되어 있어 해당 인터페이스가 적용된 객체는 value가 제네릭으로 넘겨받은 T로 적용되어야 함
interface CustomStorage<T> {
    [key: string]: T
}

// 클래스 정의
// 제네릭을 지정함으로써 new 키워드를 사용할 때, 특정 타입을 넘겨 받음
class LocalStorage<T> {
	  // 넘겨받은 제네릭은 storage 프로퍼티에 지정된 인터페이스 CustomStorage에 전달 됨
    private storage: CustomStorage<T> = {}
    set(key: string, value: T) {
        this.storage[key] = value;
    }
    remove(key: string){
        delete this.storage[key];
    }
    get(key: string): T {
        return this.storage[key];
    }
    clear(){
        this.storage = {};
    }
}

// string만을 취급하는 storage
const stringStorage = new LocalStorage<string>();
// boolean만을 취급하는 storage
const booleanStorage = new LocalStorage<boolean>();
// number만을 취급하는 storage
const numberStorage = new LocalStorage<number>();

// pet interface
interface Pet {
  name: string;
  gender: 'male' | 'female';
  age: number;
  isVaccinated: boolean;
}

// 정의한 pet Interface의 type을 가지는 객체만을 취급하는 storage
const petStorage = new LocalStorage<Pet>();
// pet Interface에 맞게 해당 인스턴스를 사용해야함
petStorage.set('siru', {name: 'siru', gender: 'female', age: 7, isVaccinated: true});
```



# Reference

[Nomad Coders - TypeScript로 블록체인 만들기](https://nomadcoders.co/typescript-for-beginners/lobby)

