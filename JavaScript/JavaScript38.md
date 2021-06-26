# [드림코딩 by 엘리] JavaScript 기초 강의(8) (ES5+)

**상세 내용 [블로그](https://greedysiru.tistory.com/545) 참고**

# Array APIs

## join

* array를 구분자를 넣어 문자열로 바꿀 수 있다. 
* 구분자를 생략시, 콤마(,)가 기본값



## split

* 문자열을 구분자를 기준으로 array로 변환
* 구분자는 문자열 또는 정규표현식
* 두번째 optional parameter는 array의 size를 지정 가능



##  reverse

* array의 item 순서를 거꾸로한다.
* array 자체의 순서를 바꾸고 그 값을 return



## splice

* 첫번째 parameter: start index
* 두번째 parameter: 지울 item의 개수
* 배열 자체는 삭제를 적용하고 return으로는 삭제된 item이 나온다.



## slice

* array의 일정 부분을 return
* 두 개의 optional parameter
  * 시작 index
  * 끝 index(해당 index의 전까지)
* array 자체를 바꾸지 않는다.



## find

```JavaScript
const result = array.find((value) => value === 90);
```

* array에서 특정 조건을 만족하는 첫번째 item을 return
* 찾지 못하면 undefined를 return
* 콜백함수는 array의 모든 item마다 호출이 되어진다.
* 호출된 콜백함수가 true이면 해당 item을 return
* 콜백함수는 boolean을 return해야한다.



## filter

```JavaScript
const new_array = array.filter((value) => vlaue === ture);
```

* 콜백함수를 true로 만족하는 item을 모아 array로 생성



##  map

```JavaScript
const new_array = array.map((value) => value * 2);
```

* array의 item 하나씩을 콜백함수를 통해 가공하여 새로운 array로 생성



## some

```JavaScript
const check = array.some((value) => value > 50);
```

* array의 item 중에서 콜백함수를 true로 return되도록 하는 요소가 있는지 boolean으로 return



## every

```JavaScript
const check = array.every((value) => value < 50);
```

* array의  모든 item이 콜백함수를 충족하는지 여부를 boolean으로 return



## reduce

```JavaScript
const result = array.reduce((prev, curr) => {
  // 다음 순서에서 prev로 받아진다.
  return prev + curr;
}, 0);
```

* 콜백함수와 초기값을 전달
* 콜백함수는 array의 모든 item에서 실행
* 콜백함수에서 이전값과 현재값을 받을 수 있다.
  * 이전값을 접근하기 위해서는 현재값을 return으로 넘겨야 한다.
* 누적합을 구할 때 주로 사용할 수 있다.
* reduceRight은 array의 제일 뒤부터 시작



## sort

```JavaScript
array.sort((a, b) => b - a);
```

* 콜백 함수에 a, b(이전값, 현재값)이 전달
* -값을 return하면 첫번째가 뒤보다 작다고 간주되어 정렬된다.



# Reference

[드림엘리 코딩 - 자바스크립트 기초 강의](https://www.youtube.com/watch?v=wcsVjmHrUQg&list=PLv2d7VI9OotTVOL4QmPfvJWPJvkmv6h-2&index=1)