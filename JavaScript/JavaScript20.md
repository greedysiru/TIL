# [코드잇] 프로그래밍 핵심 개념 in JavaScript (3)(2021.2.13)



**상세 내용 [블로그](https://greedysiru.tistory.com/201?category=860707) 참고**



# 제어문

## 01. if문

* **특별한 조건에 따라 코드를 실행**
* **else:if문의 조건을 충족하지 않을 경우 실행하는 코드**

> if (조건부분) {
>
> ​        동작부분
>
> } else {
>
> ​        동작부분
>
> }



## 02. else if 문

* **두 가지 이상의 선택지가 필요한 경우 사용**

> if (조건부분) {
>
> ​        동작부분
>
> } else if (조건부분) {
>
> ​        동작부분
>
> } else {
>
> ​        동작부분
>
> }



## 03. switch문

* **어떤 값을 입력했는지에따라 다르게 동작한다.**
  * **비교할 값과 조건값이 일치할 때** 동작부분을 수행한다.
  * **break**를 만나기 전까지 **모든 동작을 실행**한다.
  * **default :** 비교할 값이 모든 조건값과 일치하지 않을 때 수행 (생략가능)

```JavaScript
switch(비교할_값){
  case 조건값_1:
    동작부분;
    break;
  case 조건값_2:
    동작부분;
    break;
  default:
    동작부분;     
}
```



## 04. if문 vs. switch문

* **어떤 넓은 범위를 만족하는 조건식** -> if문
* **특정한 값에 일치하는 조건** -> swtich
  * 암시적 형 변환을 허용하지 않는다.
  * if문으로 대체시, **===으로 일치비교 해야한다.**



## 05. for문

* **코드를 반복하여 수행할 수 있다.**
* **조건부분이 충족(True)되면** 계속해서 반복
  * 불린으로 판별

> for (초기화부분; 조건부분; 추가동작부분) {
>
> ​        동작부분
>
> }



### 예시

```JavaScript
for (let = i; i <= 10; i++){
  console.log(`${i}번 출력`);
}
```

* **i : 반복 횟수를 저장할 변수**



## 06. for문 tip

* 추가동작부분을 꼭 채울 필요는 없다.
  * 동작부분에서 i를 증가시켜도 된다.
* 초기화부분에서 **생성한 변수는 for문의 로컬변수**이다.
* 초기화부분을 생략하고, 글로벌 변수를 활용할 수 있다.
  * 단, for문의 소괄호 안의 세미콜론은 **반드시 2개**가 필요하다.



## 07. for문 퀴즈

* 주어진 높이(height)에 맞게 삼각형을 그리는 함수 만들기

```JavaScript
function printTriangle(height) {
	for(let i = 1; i <= height; i++){ // 주어진 높이만큼 반복
	  let astarisk = ""; // 별표를 넣을 변수 선언
	  for(let j = 1; j <= i; j++){ // 각 층수만큼 별표 넣어주기
	    astarisk += '*';
	  }
	  console.log(astarisk); // 별표 출력
	}
}

// 테스트 코드
console.log('높이: 1');
printTriangle(1);

console.log('높이: 3');
printTriangle(3);

console.log('높이: 5');
printTriangle(5);
```



## 08. while문

* **조건부분을 만족하면 동작부분 반복**
* for문과 서로 대체 가능
* 반복 횟수를 저장할 변수를 글로벌 변수로 선언
* 동작부분에 반복 횟수를 증가시킬 것
* 글로벌 변수를 조건 비교에 사용하고 반복문 내부에서 다루면서 종료 후에도 변수를 사용할 경우에 유용
  * ex. 홀수 구하기

> while (조건부분) {
>
> ​        동작부분
>
> }



### 예시

```JavaScript
let i = 1;
while (i <= 10) {
  console.log(`${i}번 출력`);
  i++;
}
```



## 09. break와 continue

* **break: switch문이나 반복문을 빠져나간다.**
* **continue: 반복문의 동작부분을 건너뛴다.**
  * continue를 만나면, 반복문으로 다시 올라간다.
  * while의 경우, 무한루프에 빠지지 않도록 주의



### continue 예시

```Javascript
for (let i = 1; i <= 10; i++){
  if (i % 2 === 0) {
    continue;
  }
  console.log(i);
}
// 짝수인 경우는 continue로 인해, 출력되지 않는다.
// 1부터 10까지 홀수가 출력
```



# Reference

[코드잇 - 프로그래밍 기초 in JavaScript](https://www.codeit.kr/courses/intro-to-programming-in-javascript)