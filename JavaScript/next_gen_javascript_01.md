# Next-Gen JavaScript - Exports & Imports



**본 내용은 Udemy의 React 완벽 가이드 with Redux, Next.js, TypeScript 강의를 토대로 작성하였습니다.**



## Exports & Imports

* 모듈 방식의 코드를 작성할 수 있는 기능
* 여러 개의 파일로 코드를 분할할 수 있음
* 다른 파일에서 컨텐츠를 불러올 수 있고, JavaScript 파일은 그 컨텐츠가 어디에서 온 것인지 알 수 있음
* 모든 브라우저에서 작동하지는 않음



### 예시

```JavaScript
// person.js
const person = {
  name: 'Jaemin'
}

// default: import를 하는 곳에서 항상 default export가 내보낸 것을 기본값으로 가져옴
export default person;
```

```JavaScript
// utility.js

// named export
export const clean = () => {...}

export const baseData = 10;
                            
export const name = 'james';
```

```JavaScript
// app.js

// default export가 내보낸 것을 기본값으로 가져옴
import person from './person.js';
// 원하는대로 import한 객체 이름을 정의할 수 있음
import prs from './person.js';

// 가져올 것을 정확한 이름을 중괄호로 감싸 가져옴
import {baseData} from './utility.js';
import {clean} from './utility.js';
// as 키워드로 별칭을 지정할 수 있음
import {name as james} from './utility.js';
// *로 모든 것을 import할 수 있음
// all을 JavaScript를 객체처럼 취급하여 필요한 것을 사용할 수 있음(ex. all.clean())
import * as all from './untility.js';
```






## Reference

[[Udemy] React 완벽 가이드 with Redux, Next.js, TypeScript](https://www.udemy.com/course/best-react/)

