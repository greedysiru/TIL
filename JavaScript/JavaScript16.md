# [프로그래머스] Hello, JavaScript: 자바스크립트 입문 (2) (2021.1.29)



**상세 내용 [블로그](https://greedysiru.tistory.com/150) 참고**



# Part6. Array

## 1. 배열 만들기

### 배열

* 값을 저장할 수 있는 엘리먼트(변수)의 연속된 공간.
* 주소(index)를 이용해 각 엘리먼트에 접근 가능.



### 배열 정의

> 빈 배열 : var arr = [ ];
>
> 초기화된 배열 : var arr = [1, 2, 3, 4, 5];
>
> 어떤 자료형이든 저장가능
>
> var mixed_arr = [1, true, 3.14, "string", {name : "object" }, [1, 2, 3] ];



### 배열 길이

* **.length** 사용



### 배열 접근

* 대괄호 안에 인덱스 사용

> arr[index];

* 인덱스는 0부터 센다.



## 2. 배열 사용하기

### 배열 엘리먼트 추가 / 삭제

* **.push(element)** : 배열의 뒤에 엘리먼트 추가
* **.pop()**: 배열의 뒤에서 엘리먼트 삭제하고 리턴
* **.shift()**: 배열의 앞에서 엘리먼트 삭제하고 리턴
* **.unshift(element)**: 배열의 앞에 엘리먼트 추가



### 배열 붙이기, 검색

* **arr1.concat(arr2)** : arr1과 arr2을 붙이고 return
* **arr.indexOf(element)** : arr에서 element가 있는 첫 위치를 검색
* **arr.lastIndexOf(element)**: arr에서 element가 있는 마지막 위치를 검색



### 문자열 나누기

* **.split(구분자)**:문자열을 구분자(separator)로 나눠서 각각을 담는 배열을 변환하는 함수

```JavaScript
var str = "1, 2, 3, 4, 5";
arr = str.split(","); // arr = ["1", "2", "3", "4", "5"];
```



# Part7. 주석

* 코드에 대한 설명등의 이유로 작성하는 프로그램 동작과 무관한 코드
* 상황에 따라 일부분의 코드를 비활성화
* **//** : 한줄 주석
* **/* */** : 여러줄 주석, 보통 코드의 상단에 프로그램의 대한 설명, 라이센스에 대한 명시, 작성자에 대한 정보를 쓴다.



# Part8. 조건문

* 조건에 따라 프로그램의 흐름을 분기해서 특정 코드가 실행되게 한다.

## 1. If, else if , else

* if

> if(조건식){
>
> ​               참인경우 실행할 코드
>
> }

* else if : if문이 거짓일 때 실행

> else if(조건식){
>
> ​                       참인 경우 실행할 코드
>
> }

* else: 모든 if, else if가 거짓일 때 실행

> else{
>
> ​        실행할 코드
>
> }



## 2. switch문

* 조건에 따라 프로그램의 흐름을 분기하여 특정 코드를 실행한다.



### switch, case, break

> switch( 비교할 값 ){
>
> ​    case 값1:
>
> ​        비교할 값이 값1인 경우 실행할 코드
>
> ​        break;
>
> ​    case 값2:
>
> ​        비교할 값이 값2인 경우 실행할 코드
>
> ​        break;
>
> ​            ......
>
> ​    default:
>
> ​        비교할 값이 위의 모두와 다를 경우 실행할 코드
>
> ​        break;
>
> }

* **break**: break 구문을 만나면, switch를 빠져나온다.
  * 사용하지 않으면, 다음 case까지 실행해버린다.



# Part9. 반복문

* 조건에 따라 프로글매의 일정 코드를 반복적으로 수행

## 1. while

* 조건이 만족하는 동안 코드를 반복 실행

> while (조건식) {
>
> ​        반복 실행될 코드
>
> }



### 예시

```JavaScript
var count = 0;

while(true){
  var ans;
  ans = parseInt(prompt("1 + 1 = ?"));
  if (ans != 2 ){
      console.log( (++count) + "번 틀렸습니다. 다시 도전하세요.");
      continue;
  }
  ans = parseInt(prompt("7 - 3 = ?"));
  if (ans != 4){
      console.log( (++count) + "번 틀렸습니다. 다시 도전하세요.");
      continue;
  }
  ans = parsInt(prompt("9 * 7 = ?"));
  if (ans != 63){
      console.log( (++count) + "번 틀렸습니다. 다시 도전하세요.");
      continue;
  }
  
  break;
  
  // continue를 만나면 여기로 이동
  
}

// break를 만나면 여기로 이동

console.log("참 잘했습니다.");
```

* **continue**: 남은 반복 실행 코드를 모두 넘어간다.



## 2.  do while

* 한 번은 코드를 실행하고 반복 실행될지 결정한다.

> do {
>
> ​       반복 실행될 코드
>
> }while(조건식);



### 예시

```JavaScript
do{
    var ans = parseInt(prompt("1+1=?"));
}while( ans != 2 ); // 문제를 틀리면 참이므로 맞출 때까지 실행한다.

console.log("맞췄습니다.");
```



## 3. for

* 초기구문, 업데이트 구문, 반복조건을 한 구문에 합친 반복문

> for ( 초기구문 ; 반복 조건; 업데이트 ){
>
> ​        실행할 코드
>
> }

* 초기구문은 항생 실행된다.
* 조건이 참이 아니면 반복문이 종료된다.
* **break**와 **continue**를 사용할 수 있다.
* **contiune**문을 만나면 업데이트문으로 돌아간다.
  * cf ) **while**문에서는 **continue**문을 만나면 반복실행 코드의 끝으로 이동한 뒤 조건식을 검사한다.



### 예시

```JavaScript
var array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

for ( var i = 0; i < array.length ; i++ ){ // 조건식
    console.log( array[i] );     // 반복 실행될 코드  
}
```



## 4. for in

* 객체의 각 엘리먼트에 접근할 수 있는 반복문
* 배열에서도 사용할 수 있다.
* **in** : 단독 사용시, 속성의 이름이 객체에 존재하는지 boolean으로 return



### 예시

* 객체의 속성을 출력

```JavaScript
var obj = {
    name : "object",
    weight : 30,
    isObject : true,
    arr: [1, 2, 3],
    obj:{property:1}
};

for( var propertyName in obj ){
    console.log( "\t", propertyName, ": ", obj[propertyName] );
}
```

* 객체의 key들을 변수에 담아 한 개씩 접근할 수 있다.

<br>

* 아래처럼 for문에서도 위와 같이 객체의 속성을 출력할 수 있다.

```JavaScript
var obj = {
    name : "object",
    weight : 30,
    isObject : true,
    arr: [1, 2, 3],
    obj:{property:1}
};
var property_list = Object.keys(obj);

for( var i=0 ; i<property_list.length ; i++ ){
    var propertyName = property_list[i];
    console.log( "\t", propertyName, ": ", obj[propertyName] );
}
```

* **Object.keys()**: 객체의 key에 접근하여 리스트 형태로 return하는 메소드



# Part10. 더 알아보기

## 1. 변수의 scope

* **scope** : 선언한 변수가 유효한 영역
* **function scope**
  * **선언딘 변수는 선언된 함수 안에서 접근 가능**
  * 선언된 함수 안에서 선언된 함수에서도 접근 가능



## 2. 변수의 shadowing

* 함수의 안에서 밖에서도 선언되었던 같은 이름의 변수를 사용하는 경우
  * 함수 밖의 변수는 가려짐(**shadowing**)
  * 함수 안에서는 해당 함수에서의 변수를 사용 (함수 밖 변수의 값은 변하지 않음)
  * 함수에서 빠져나오면 다시 해당 변수에 접근할 수 있다.
* 함수 안에서 값이 유지되어야 할 때
  * **함수 내부에서 var키워드를 사용해서 선언**
* 여러 함수에서 값이 유지되면서 사용되는 변수의 경우
  * **함수를 포괄하는 곳에서 선언하고 사용**



## 3. method, this

* **method**:객체 속성의 값으로서 들어간 함수
* **this**:함수가 호출되었을 때 어떤 객체에 bind된 속성으로서 불렸는지 알려준다.
  * 일반적인 함수 호출은 전역객체(브라우저의 경우 window)에 바인딩 된다.
  * 메소드로서 호출되었을 때 해당 객체가 나오게 된다.



## 4. closure

* 함수, 함수가 선언될 때의 environment로 구성된다.
* 함수가 정의 될 떄의 environment가 함꼐 closure로 결합된다.

```JavaScript
function makeCounterFunction(initVal){
    var count = initVal;
    function Increase(){
        count++;
        console.log(count);
    }
    return Increase;
}

var counter1 = makeCounterFunction(0); // var count = 0;
var counter2 = makeCounterFunction(10); // var count = 10;
```



# Reference

https://programmers.co.kr/learn/courses/3