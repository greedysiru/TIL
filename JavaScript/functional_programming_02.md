# 함수형 프로그래밍과 ES6+ - 리스트 순회 ES5 vs. ES6+



**본 내용은 프로그래머스의 함수형 프로그래밍과 ES6+ 강의를 토대로 작성하였습니다.**



## 리스트 순회 ES5 vs. ES6+

* 간결하고 선언적인 방식으로 변경 됨

### ES5

```JavaScript
// array
const list = [1, 2, 3];
for (var i = 0; i < list.length; i++) {
  console.log(list[i]);
}

// array-like
const str = 'abc';
for (var i = 0; i < str.length; i++) {
  console.log(str[i]);
}
```



### ES6+

```JavaScript
// array
const list = [1, 2, 3];
for (const li of list) {
  console.log(li);
}

// array-like
const str = 'abc';
for (const s of str) {
  console.log(s);
}
```





## Reference

[[프로그래머스] 함수형 프로그래밍과 ES6+](https://school.programmers.co.kr/learn/courses/7637)

