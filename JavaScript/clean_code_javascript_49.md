# 클린코드 자바스크립트 - 함수 다루기(화살표 함수)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 화살표 함수

### 화살표 함수의 특징

* Lexical Scope를 가짐
  * 상위의 스코프를 따름
  * 기존  함수 this와 다르게 동작
  * 메서드로 사용할 수 없음
* arguments 객체를 가지지 않음
  * Rest Parameter를 사용하기
* call, apply, bind를 사용할 수 없음
* 생성자 함수로서 사용할 수 없음
* class 문법에서
  * 부모 클래스의 메서드가 화살표 함수로 선언되어 있는 경우, 자식 클래스에서 사용할 수 없음
  * override를 불가능
* generator의 yield 키워드 뒤에 사용 불가

```JavaScript
const cat = {
  name: 'siru',
  // 아래 메서드들은 화살표 함수로 정의되어 동작하지 않음
  getName: () => {
    return this.name
  },
  newFriends: () => {
    const newFriendsLilst = Array.from(arguments);
    return this.name + newFriendList;
  }
};
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

