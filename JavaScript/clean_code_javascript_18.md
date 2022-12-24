# 클린코드 자바스크립트 - 분기 다루기(단축평가)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. 단축평가란

* AND, OR 연산자를 활용하여 좌항에서 우항까지로의 값을 평가 
* 조건부로 특정 값을 평가시킬 수 있음



### AND

* AND연산에서는 피연산자가 모두 참이어야 참으로 귀결 됨
* 왼쪽으로부터 참이면 우항으로 이동
* 거짓이 확인되면 중단하고 거짓으로 귀결

```JavaScript
true && true && '도달'; // '도달'

true && false && '도달'; // false
```



### OR

* OR연산에서는 피연산자 중 하나라도 참이면 참으로 귀결
* 왼쪽으로부터 거짓이면 우항으로 이동
* 참이 확인되면 중단하고 참으로 귀결

```JavaScript
true || false || '도달'; // '도달'

true || true || '도달'; // true
```



## 2. 단축평가 응용

* 조건부처리를 단축평가로 할 수 있음
* AND: 선제적인 조건(좌항)이 true이어야 할 때 용이
* OR: default value를 표현할 때 용이



### AND예시

```JavaScript
const getCatName = (isCat, catInformation) {
  // 둘 다 참이어야만 실행
  if (isCat && catInformation) {
    const {name} = catInformation;
    // OR 단축 평가
    return name || '고양이 이름 없음';
  }
}
```





### OR예시

```JavaScript
const fetchData = async () => {
  const response = await fetchAPI();
  // response가 undefined(Falsy)라면 우항의 문자열을 return
  return response || '불러오는 중...';
}
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)