# ES Modules

**본 내용은 노마드 코더님의 Export Default 과연 제대로 알고계십니까? 강의를 토대로 작성하였습니다.**



## 1. 모듈

* 코드를 파일 단위로 나누어 모듈화
* 코드를 모듈화하여 사용하는 것이 편리성, 유지보수 측면에서 좋음
* 다이나믹 모듈을 이용하면 애플리케이션 로딩을 빠르게 할 수 잇음
* import, export 하여 사용



## 2. Named Export & Syntax Import

### Named Export

* Math.js 모듈에서 각기 다른 3개의 함수를 export

```JavaScript
// math.js
export const plus = (a, b) => a + b;
export const minus = (a, b) => a - b;
export const divide = (a, b) => a / b;
```



### Syntax Import

* Named Export 된 함수를 import하려면 Syntax Import 사용
* 중괄호 사이에는 import 할 함수명을 쓸 수 있음
* import할 함수명과 export 될 함수명은 반드시 같아야 함

```JavaScript
// main.js
import {plus} from "./math";
```



### as 키워드

* import한 함수 명을 as 키워드로 바꿀 수 있음

```JavaScript
// main.js
import {plus as add} from "./math";
```



## 3. Default Export & Import

* 각 파일마다 단 한개의 Default Export만 존재
* import하기 더 간단해짐
* 모듈 내 함수가 들어있는 객체를 원하는 이름으로 불러올 수 있음



### Defalut Export

* 모듈 내 모든 함수를 한개의 객체로 Default Export

```JavaScript
// math.js
const plus = (a, b) => a + b;
const minus = (a, b) => a - b;
const divide = (a, b) => a / b;

export default {plus, minus, divide}
```

<br/>

* 단 한개의 함수만 export할 때도 사용

```JavaScript
// db.js
const connectToDB = () => {/*magic*/};
export default connectToDB;
```



### Default Import

* 모듈을 import하여 모듈내의 함수를 사용할 수 있다.
* import 키워드 다음에 원하는 이름으로 바꿀 수 있다.

```JavaScript
// main.js
import myMath from "./math";

myMath.plus(2, 2);
```



## 4. Named Export 와 Default Export 혼용

### export

```JavaScript
const connectToDB = () => {/*magic*/};
export const getUrl = () => {/*magic*/};
export default connectToDB;
```



### import

```JavaScript
import connect, {getUrl} from './db';
```



## 5. Star Import

* 모든 exported 된 내용을 Import
* Default Export가 없어야 함



### export

```JavaScript
// math.js
export const plus = (a, b) => a + b;
export const minus = (a, b) => a - b;
export const divide = (a, b) => a / b;
```



### import

* Syntax Import 를 사용하여 모든 내용을 Import
* Asterisk === everything
* 모듈의 함수들을 불러와서 myMath 객체에 넣음

```JavaScript
import * as myMath from "./math";

myMath.plus(2, 2);
```



## 6. 모듈 로딩을 빠르게 하는 방법

* 필요한 것만 Import

  * Named Export하여 필요한 것만 Syntax Import
  * Named Export로 함수를 정리하는 것이 권장

  

### Dynamic Import

* 기존 Import는 파일의 위에서부터 모든것을 Import
  * 사용하든 안하든 웹사이트의 모든 코드를 모두 다운받아야 하므로 로딩속도를 늦춤
* Dynamic Import는 실제 유저가 사용할 모듈만 Import



### Dynamic Import 예시

```JavaScript
async function doMath() {
  // 유저가 클릭시에만 모듈을 가져옴
  const math = await import("./math");
  math.plus(2, 2);
}

btn.addEventListener("click", doMath);
```



# Reference

[[노마드 코더] ES Modules](https://www.youtube.com/watch?v=WUirHxOBXL4&t=5s)