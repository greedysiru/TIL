# 16장 - 프로퍼티 어트리뷰트(2)

**본 내용은 모던 자바스크립트 Deep Dive - 자바스크립트의 기본 개념과 동작 원리를 토대로 작성하였습니다.**



## 16.3 데이터 프로퍼티와 접근자 프로퍼티

### 16.3.1 데이터 프로퍼티

* 키와 값으로 구성된 접근 가능한 일반적인 프로퍼티
* 데이터 프로퍼티의 프로퍼티 어트리뷰트
  * 프로퍼티 초기화시 모두 true

| 프로퍼티 어트리뷰트 | 프로퍼티 디스크립터 객체의 프로퍼티 | 설명                                                         |
| ------------------- | ----------------------------------- | ------------------------------------------------------------ |
| [[Value]]           | value                               | 값<br />기존 값이 존재하면 재할당<br />값이 없으면 프로퍼티 동적 생성 |
| [[Writable]]        | writable                            | 값의 **변경 가능 여부**<br />불리언<br />false -> 읽기 전용 프로퍼티 |
| [[Enumerable]]      | enumerable                          | 프로퍼티의 **열거 가능 여부**<br />불리언                    |
| [[Configurable]]    | configurable                        | **재정의 가능 여부**<br />false -> 프로퍼티의 삭제, 프로퍼티 어트리뷰트 값 변경 금지 |



### 16.3.2 접근자 프로퍼티

* 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 **접근자 함수**로 구성된 프로퍼티
* getter/setter
* getter의 방식
  * 프로퍼티 키 유효 확인(문자열 또는 심벌)
  * 프로토타입 체인에서 프로퍼티 검색
  * 데이터 프로퍼티인지 접근자 프로퍼티인지 확인
  * 결과 반환

| 프로퍼티 어트리뷰트 | 프로퍼티 디스크립터 객체의 프로퍼티 | 설명                                                         |
| ------------------- | ----------------------------------- | ------------------------------------------------------------ |
| [[Get]]             | get                                 | 접근자 함수<br />getter 함수가 호출되어 프로퍼티 값으로 변환 |
| [[Set]]             | set                                 | 데이터 프로퍼티의 값을 저장할 때 호출되는 접근자 함수<br />setter 함수가 호출되고 프로퍼티 값으로 저장 |
| [[Enumerable]]      | enumerable                          | 데이터 프로퍼티와 동일                                       |
| [[Configurable]]    | configurable                        | 데이터 프로퍼티와 동일                                       |

```JavaScript
const cat = {
  name: 'Siru',
  churuLike: true,
  
  // 접근자 프로퍼티
  get printChuruLike() {
    if (this.churuLike){
    	return `${this.name}는 츄르를 좋아합니다.`;  
    } else {
      return `${this.name}는 츄르를 안 좋아합니다.`;
    }
  },
  
  set changeChuruLike(flag) {
    this.churuLike = flag;
  }
};

console.log(cat.printChuruLike); // Siru는 츄르를 좋아합니다.
cat.changeChuruLike = false;
console.log(cat.printChuruLike); // Siru는 츄르를 안 좋아합니다.
```

