# Refactoring - 기본적인 리팩터링(1)

**본 내용은 마틴 파울러의 Refactoring 2판을 토대로 작성되었습니다.**



## 기본적인 리팩터링

* 가장 기본적이고 많이 사용하는 리팩터링 기법들



## 1. 함수 추출하기

* 반대 리팩터링: 함수 인라인하기



### 예시 코드

```JavaScript
function printOwing(invoice) {
  printBanner();
  let outstanding = calculateOutstanding();
  
  // 세부 사항 출력
  console.log(`고객명: ${invoice.customer}`);
  console.log(`채무액: ${outstanding}`);
}
```



```JavaScript
function printOwing(invoice) {
  printBanner();
  let outstanding = calculateOutstanding();
  printDetails(outstanding);
  
  function printDetails(outstanding) {
    console.log(`고객명: ${invoice.customer}`);
    console.log(`채무액: ${outstanding}`);
  }
}
```



### 설명

* 가장 많이 사용되는 리팩터링
* 코드 조각을 찾아 무슨 일을 하는지 파악한 후, 독립된 함수로 추출하고 목적에 맞는 이름을 붙임
* 기준
  * 코드의 길이
  * 재사용성
  * **목적과 구현을 분리**
* 코드를 보고 무슨 일을 하는지 파악하는 데 한참이 걸린다면 그 부분을 함수로 추출한 뒤 '무슨 일'에 걸맞는 이름을 짓기
  * 코드를 다시 읽을 때 함수의 목적이 눈에 확 들어옴
  * 본문코드를 신경 쓰지 않아도 됨
* 함수를 대체로 아주 짧게(단 몇 줄) 작성
* 함수 호출이 많아져서 성능이 느려지지 않음
  * 함수가 짧으면 캐싱하기가 더 쉽기 때문에 컴파일러가 최적화하는 데 유리
* 주석이 있는 경우 주석을 참고하여 이름 짓기



### 절차

1. 함수를 새로 만들고 목적을 잘 드러내는 이름을 붙임
   - 이름이 떠오르지 않는 경우, 함수로 추출하면 안 된다는 신호
   - 중첩함수를 지원하는 언어인 경우 원래 함수 안에 중첩
2. 추출한 코드를 원본 함수에서 복사하여 새 함수에 붙여 넣기
3. 추출한 코드 중 원본 함수의 지역 변수를 참조하거나 추출한 함수의 유효범위를 벗어나는 변수는 없는 지 검사하기
4. 변수를 다 처리 후, 컴파일
5. 원본 함수에서 추출한 코드 부분을 새로 만든 함수를 호출하는 문장으로 바꿈
6. 테스트
7. 다른 코드에 추출한 함수와 똑같거나 비슷한 코드가 없는 지 살피고 있으면 추출한 새 함수를 호출할 지 검토



## 2. 함수 인라인하기

* 반대 리팩터링: 함수 추출하기



### 예시 코드

```JavaScript
function getRating(driver) {
  return moreThanFiveLateDeliveries(driver) ? 2 : 1;
}

function moreThanFiveLateDeliveries(driver) {
  return driver.numberOfLateDeliveries > 5;
}
```



```JavaScript
function getRating(driver) {
  return (driver.numberOfLateDeliveries > 5) ? 2 : 1;
}
```



### 설명

* 함수 본문이 이름만큼 명확한 경우도 있음
* 또는 함수 본문 코드를 이름만큼 깔끔하게 리팩터링할 때도 있음
* 간접 호출을 너무 과하게 쓰는 코드도 흔한 인라인 대상
* 다른 함수로 단순히 위임하기만 하는 함수들이 너무 많아서 위임관계가 복잡하면 인라인 하기



### 절차

1. 다형 메서드인지 확인
   - 서브클래스에서 오버라이드하는 메서드는 인라인하면 안 됨
2. 인라인할 함수를 호출하는 곳을 모두 찾음
3. 각 호출문을 함수 본문으로 교체
4. 하나씩 교체할 때마다 테스트
5. 함수 정의를 삭제



## 3. 변수 추출하기

* 반대 리팩터링: 변수 인라인하기



### 예시 코드

```JavaScript
return order.quantity * order.itemPrice -
  Math.max(0, order.quantity - 500) * order.itemPrice * 0.05 +
  Math.min(order.quantity * order.itemPrice * 0.1, 100);
```



```JavaScript
const basePrice = order.quantity * order.itemPrice;
const quantityDiscount = Math.max(0, order.quantity - 500)
												* order.itemPrice * 0.05;
const shipping = Math.min(basePrice * 0.1, 100);
return basePrice - quantityDiscount + shipping;
```



### 설명

* 표현식이 너무 복잡한 경우
  * 지역변수를 활용하여 표현식을 쪼개 관리하기 더 쉽게 만듦
* 구성 단계마다 이름을 붙임
* 추가한 변수들은 디버깅에서도 도움이 됨
  * 중단점을 지정하거나 상태를 출력하는 문장을 추가
* 현재 함수에서만 의미가 있으면 변수로 추출
* 함수를 벗어난 넓은 문맥에서까지 의미가 된다면, 넓은 범위에서 통용되는 이름을 생각하기
  * 함수로 추출



### 절차

1. 추출하려는 표현식에 부작용은 없는지 확인
2. 불변 변수를 하나 선언하고 이름을 붙일 표현식의 복제본을 대입
3. 원본 표현식을 새로만든 변수로 교체
4. 테스트
5. 표현식을 여러 곳에서 사용하면, 새로 만든 변수로 교체하고 그 떄마다 테스트



## 4. 변수 인라인하기

* 반대 리팩터링 : 변수 추출하기



### 설명

* 변수는 함수 안에서 표현식을 가르키는 이름
  * 하지만, 그 이름이 표현식과 다를 바가 없을 때 변수를 인라인하기



### 절차

1. 대입문의 우변(표현식)에서 부작용이 생기지는 않는지 확인
2. 변수가 불변으로 선언되지 않았다면 불변으로 만든 후 테스트
3. 변수를 가장 처음 사용하는 코드를 찾아서 대입문 우변의 코드로 바꿈
4. 테스트
5. 변수를 사용하는 부분을 모두 교체할 때까지 이 과정을 반복
6. 변수 선언문과 대입문을 지움
7. 테스트