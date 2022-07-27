# React Hook Form(1)

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## 1. React Hook Form?

* React에서 Form을 간단하게 다룰 수 있게 하는 라이브러리
* 많은 input 요소를 효율적으로 관리할 수 있음
* Validation 지원



## 2. useForm

* form을 사용하기 위한 함수들을 return하는 hook
  * register: input을 등록
  * watch
  * handleSubmit
  * formState
  * setError
  * setValue



### 예시

* TypeScript와 함께 사용할 때는 제네릭으로 form data의 interface를 전달해야 함

```TypeScript
import React from "react";
import { useForm } from "react-hook-form";

// form data의 interface
interface IOrderForm {
  name: string;
  phoneNumber: string;
  phoneNumberConfirm: string;
}

function OrderPage {
  
  // useForm을 호출하여 필요한 함수들을 가져올 때, 제네릭으로 interface를 전달해야 type이 적용 됨
  const {
    register,
    handleSubmit,
    formState: {errors},
    setError,
  } = useForm<IOrderForm>({
    // 해당 form data에 대한 default value 지정
    defaultValues: {
      phoneNumber: "010-0000-0000",
      phoneNumberConfirm: "010-0000-0000",
    }
  })
  
  return (
  	// JSX
    // inputs
  )
  
}
```



## 3. register

* input을 등록
* 첫 번째 파라미터는 input을 구분하기 위한 name
* 두 번째 파라미터는 options
  * **해당 input의 validation을 정의할 수 있음**
  * 정규 표현식을 전달할 수 있음
* 사용할 input에서 호출해야 함
* required가 지정된 input에 입력이 안 된 경우, 해당 input으로 자동 커서 이동처리가 됨



### 예시

```React
return (
	<form>
  	<input
          {...register("name", {
     				// 필수값으로 지정, 입력하지 않은 경우 아래 문자열로 error message 발생
            required: "이름은 필수 값입니다.",
      			// Costum Validation을 정의할 수 있음
            validate: {
              // 함수 명: Validation 규칙 명
              // 해당 input에 입력된는 값을 인자로 받음
              // true or false를 반환
              // async로 정의하여 서버 API와 연동할 수 있음
              noJames: (value) =>
                value.includes("James") ? "James는 사용할 수 없는 이름입니다." : true,
            },
			      // 글자수 제한 Validation
      			minLength: {
              value: 4,
              // 지키지 않은 경우의 메시지(error)
              message: "4글자 이상 입력하셔요 합니다."
            }
          })}
          placeholder="name"
      />
      <input
            {...register("phoneNumber", {
            required: "핸드폰 번호는 필수 값입니다.",
            // 정규표현식을 통과하지 못하면, error 발생
            pattern: {
              value: /^\d{3}-\d{3,4}-\d{4}$/,
              message: "올바른 형식의 번호가 아닙니다.",
            },
          })}
        	placeholde="phone"
        />
    <input
            {...register("phoneNumberConfirm", {
            required: "핸드폰 번호를 확인해주세요.",
            // 정규표현식을 통과하지 못하면, error 발생
            pattern: {
              value: /^\d{3}-\d{3,4}-\d{4}$/,
              message: "올바른 형식의 번호가 아닙니다.",
            },
          })}
        	placeholde="phone confirm"
        />
  </form>
)
```

# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)
