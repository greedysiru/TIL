# 클린코드 자바스크립트 - 배열 다루기(고차 함수로 리팩터링)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 고차함수로 리팩터링

* for문으로 배열을 접근하는 로직을 사용하기 보다 고차함수를 활용하여 명시적인 코딩하기



### 예시1

```JavaScript
const cats = ['siru', 'nunu', 'mango', 'meonji', 'cong'];

// for문을 사용한 로직
const callAllCats = (catList) => {
  let temp = [];
  
  // 로직을 파악하기 위해 for문을 분석해야 함
  for (let i = 0; i < catList.length; i++) {
    temp.push(catList[i] + ' 이리와');
  }
  
  return temp;
}

// 고차함수로 리팩터링한 로직
// 명시적이고 로직을 파악하기 쉬움
const addComeOn = (name) => name + ' 이리와'; 

const callAllCats = (catList) => catList.map(addComeOn);
```



### 예시2

* 위 함수에서 특정 조건을 만족해야하는 요구 사항 추가
  * 입력받은 고양이만 불러야 함

```JavaScript
// ...

// for문을 사용한 로직
const callMyCat = (catList, catName) => {
  let temp = [];
  
  for (let i = 0; i < catList.length; i++) {
    const currentItem = catList[catName];
    // 특정 고양이만 가져오기
    if (currentItem === catName) {
			temp.push(catList[i] + ' 이리와'); 
    }
  }
  
  return temp;
}

// 고차함수로 리팩터링한 로직
const addComeOn = (name) => name + ' 이리와'; 

const callMyCat = (catList, catName) => catList.filter(cat === catName).map(addComeOn);
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)

