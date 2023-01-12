# 클린코드 자바스크립트 - 객체 다루기(Lookup Table)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## Loockup Table

* 배열에서 key, value로 관리된 배열이 나열된 형태
* JSON과 비슷한 형태
* JavaScript에서는 object + computed property를 활용하여 구현 가능
* 불필요한 분기문을 줄일 수 있음
* 상수들을 모아 파일로 관리할 때 유용



### switch-case -> lookup table

```JavaScript
// switch-case 문
function getCatType(type) {
  // 요구사항이 늘어날 때마다 복잡해질수밖에 없는 구조
  switch (type) {
    case 'siru':
      return '삼색이';
    case 'nunu':
      return '하얀 고양이';
    case 'meonji':
      return '까만 고양이';
    case 'magno':
      return '갈색 고양이';
    default:
      return '그런 고양이는 없는데요?'
  }
}

// lookup table
function getCatType(type) {
  const CAT_TYPE = {
    siru: '삼색이',
    nunu: '하얀 고양이',
    meonji: '까만 고양이',
    mango: '갈색 고양이',
  }
  
  // 단축평가로 존재하지 않은 값을 넣었을 때의 처리
  return CAT_TYPE[type] || '그런 고양이는 없는데요?';
  // nulish operator로 대체 가능
  return CAT_TYPE[type] ?? '그런 고양이는 없는데요?'; 
}
```



### 팩토리 함수로의 응용

* Lookup Table을 바로 return하는 형식으로 정의할 수 있음

```JavaScript
function getCatType(type) {
  return ({
    siru: '삼색이',
    nunu: '하얀 고양이',
    meonji: '까만 고양이',
    mango: '갈색 고양이',
  }[type] ?? '해당 없음'
 )
}
```



## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

