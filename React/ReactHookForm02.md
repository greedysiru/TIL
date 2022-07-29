# React Hook Form(2)

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**

##  1. watch

* 등록한 input의 변화를 감지하고 해당 값을 반환할 수 있음
* 첫 번째 파라미터는 register로 등록한 input name



## 2. handleSubmit

* 입력한 input data들의 유효성 검사가 성공하면 form data를 받음
* 첫번째 인자
  * valid 함수
  * form 데이터가 유효할 때만 호출되는 함수
* 두번째 인자
  * form 데이터가 유효하지 않을 때 호출되는 함수




### 예시

```React
// form datas의 interface를 전달받게 되므로 타입 지정
const onValid = (data: IOrderForm) => {
  // submit 되기 전의 data validation을 정의
  if (data.phoneNumber !== data.phoneNumberConfirm) {
    // Error를 발생
    setError(
    	"phoneNumberConfirm",
      {message: "핸드폰 번호 확인이 입력한 핸드폰 번화와 다릅니다. 확인해주세요."},
      // 유효하지 않을 때 해당 input에 커서 자동 이동
      { shouldFocus: true }
    )
  }
}

return (
	<form onSubmit=(handleSubmit(onValid))>
		<!-- inputs -->
  </form>
)
```






## 3. formState

* formState에 접근할 수 있음
* error 객체를 가짐
* 활용하여 에러 메시지를 표시할 수 있음



### 예시

```React
function OrderPage() {
  
  const {
    register,
    handleSubmit,
    // 구조 분해 할당으로 formState의 erros 객체 가져오기
    formState: {errors},
    setError,
  } = useForm<IOrderForm>({
    defaultValues: {
      phoneNumber: "010-0000-0000",
      phoneNumberConfirm: "010-0000-0000",
    }
  })
  
  return (
    <>
      <form>
        <!-- inputs -->
      </form>
      // 에러를 표시할 컴포넌트
      <NoticeError>
        <span>{errors?.name?.message}</span>
        <span>{erros?.name?.phoneNumber}</span>
      </NoticeError>
    </>
  )
}
```



## 4. setError

* 에러를 set할 수 있는 함수
* 특정 조건에서 특정 에러를 발생시킬 수 있음
* **예시는 상기 handleSubmit을 참고**

# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)