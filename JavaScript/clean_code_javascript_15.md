# 클린코드 자바스크립트 - 분기 다루기(값식문)



**본 내용은 Udemy의 클린코드 자바스크립트 강의를 토대로 작성하였습니다.**



## 1. 값식문

* 문법 에러를 방지하기 위해 문법을 공부하는 것은 중요

* 단순한 오타가 장애와 서비스 오류를 일으킴

* JavaScript에서의 값, 식, 문을 구분할 줄 알아야함

  * 문법 지식이 토대

  

## 2. if vs. 삼항연산자

* if문은 값으로 취급되지 않음
  * 객체 안에 if문으로 조건부로 값을 정의하는 것은 불가능
* 삼항연산자는 식으로 취급
  * 식은 값으로 수렴됨
  * 객체 안에 조건부로 값을 정의할 수 있음

```JavaScript
const cat = {
  name: if (isCat) 'siru', // syntax Error
}

// 삼항연산자는 조건부로 값 할당 가능
const cat = {
  name: isCat? 'siru' : '',
}
```



## 3. 즉시실행함수

* IIFE
* 값과 식만 넣어야 함

```react
<p>
	{(() => {
    switch (this.state.catName) {
        // 값을 return하기 때문에 switch 문을 사용할 수 있음
      case 'siru':
        return '나의 고양이 시루';
      case 'mango':
        return '친구 고양이 망고';
      case 'nunu':
        return '민수 고양이 누누';
    }
  })()}
</p>
```



## 4. 논리연산자

* 분기문 없이 조건부로 값을 return 시킬 수 있음

```react
<p>
  <!-- catName이 없어서 falsy -> false로 평가되면 논리연산자로 인해 '고양이가 없어'라는 문구가 뜨게 됨 -->
{this.props.catName || '고양이가 없어'}
</p>
```



## 5. for vs. map

* 여러개의 데이터들(특히 배열)을 React Elements로 변환하여 렌더링할 때는 map과 같은 고차함수를 쓰는 것이 유용



### for

```react
const cats = ['siru', 'nunu', 'mango'];
...
<p>
  {(() => {
    const spans = [];
    // cats 배열에 접근하여 각 요소에 대응되는 span element를 생성
    for (let i = 0; i < cats.lenght; i++) {
      spans.push(<span key={i}>{cats[i]}</span>)
      // return 하여 생성된 elements들을 렌더링
      return spans;
    }
  })()}
</p>
```



### map

```react
const cats = ['siru', 'nunu', 'mango'];
...
<p>
	{cats.map((cat, index) => (<span key={index}>{cat})</span>)}
</p>
```





## Reference

[[Udemy] 클린코드 자바스크립트 - Poco Jang](https://www.udemy.com/course/clean-code-js/)
