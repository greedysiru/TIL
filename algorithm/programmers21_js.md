# [프로그래머스] 소수 찾기 - JavaScript 풀이

**본 게시물은 프로그래머스의 연습 문제 풀이입니다. 저작권은 (주) 그랩에게 있습니다**

## 자바스크립트 코드(나의 풀이)

```javascript
// 소수 찾기
// 순열을 만드는 함수
function makePermutations(arr, select) {
  // 순열
  const permutations = [];
  // 1개를 택하면 모든 원소를 return
  if (select === 1) return arr.map((value) => {
    return [value]
  });

  arr.forEach((fixed, index, origin) => {
    // 매 루프에서의 fixed(value)를 제외한 나머지 원소들의 배열
    const rest = [...origin.slice(0, index), ...origin.slice(index + 1)];
    // 나머지에대한 순열들 구하기
    const restOfPermutation = makePermutations(rest, select - 1);
    // 순열을 구한 뒤, fixed 값 더하기
    const permutation = restOfPermutation.map((value) => [fixed, ...value]);
    permutations.push(...permutation);
  })

  return permutations;
}

// 소수임을 판별하는 함수
function checkPrime(number) {
  // 소수 여부를 저장하는 변수
  // 소수이면 true, true로 초기화
  let plag = true;
  // 2부터 i의 제곱이 해당 숫자 이하일 때까지 나머지가 0인지 체크
  for (let i = 2; i * i <= number; i++) {
    // 소수가 아니므로 plag를 false 처리하고 반복문 종료
    if (number % i === 0) {
      plag = false;
      break;
    }
  }
  // plag를 return
  return plag;
}

function solution(numbers) {
  let answer = 0;
  // 문자열 배열 변환
  const numbersArray = [];
  for (let i = 0; i < numbers.length; i++) {
    numbersArray.push(numbers[i]);
  }
  // 주어진 숫자로 만들 수 있는 순열
  const numberPermutations = [];
  // 순열구하기
  for (let j = 1; j <= numbers.length; j++) {
    const permutations = makePermutations(numbersArray, j);
    // 만들어진 순열 하나씩 접근
    for (let permutation of permutations) {
      // 문자열로 변환후 숫자로 변환
      const permutationNumber = parseInt(permutation.join(''));
      // numberPermutations에 없으면 넣기
      if (!(numberPermutations.includes(permutationNumber)) && permutationNumber != 0 && permutationNumber != 1) {
        numberPermutations.push(permutationNumber);
      }
    }
  }
  // numberPermutations를 하나씩 가져와서 소수인지 판별하기
  for (let numberPermutation of numberPermutations) {
    if (checkPrime(numberPermutation)) {
      answer += 1;
    }
  }

  return answer;
}
```



## Comment

주어진 `numbers`로부터 소수를 찾기 위해서크게 아래와 같은 과정을 거친다.

1. 순열만들기
2. 만들어진 순열들을 하나씩 접근해서 문자열로 변환후 정수로 변환
3. 중복이 되지 않도록 다른 배열에 옮기기
4. 만들어진 배열의 요소를 하나씩 접근하여 소수 판별하기

순열을 만들기 위해서, 순열의 대상이 되는 배열과 뽑을 수 두 개의 파라미터를 받는 순열 생성 함수를 선언한다. 이 함수는 `forEach`문으로 배열의 한 요소마다 콜백함수를 실행한다. 고정되는 요소, 나머지 요소로 이루어진 배열을 나눈다. 그리고 나머지 배열과 뽑을 수 -1을 입력하여 해당 함수를 재귀호출한다. 재귀함수의 종료 조건은 뽑을 수가 1일 때, 각자 요소를 중괄호([])를 씌워서 `return` 한다. `return`된 배열을 스프레드 문법을 활용하여 고정된 요소와 합쳐주고 리턴한다. 상세 동작은 위의 주석을 참고할 것.

만들어진 순열은 아직 배열의 형태이므로 `join`과 `parseInt` 를 사용해서 정수값으로 바꾼다. 그리고 만들어진 정수는 중복이 될 수 있으므로 `if`와 `include`를 사용해서 중복을 처리해준다.

소수를 판별할 때는, 시간복잡도를 고려한다. 해당 수의 제곱근만큼만 검사하도록 `for문`의` i * i`가 해당 수 이하일때까지만 검사하면 된다.

## Reference

[프로그래머스](https://programmers.co.kr)

