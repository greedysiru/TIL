# Recoil(2)

**본 내용은 Nomad Coders - React JS 마스터클래스 강의를 토대로 작성하였습니다.**



## 1. useRecoilState

* value, modifier 함수를 반환



### 예시

```React
import { atom, useRecoilState } from "recoil";

interface IOrderList {
  product: string;
  id: number;
  status: "배송전" | "배송중" | "배송완료";
}

// atom 정의할 때 제네릭으로 인터페이스를 전달
const orderList = atom<IOrderList[]>({
  key: "orderList",
  default: [],
});

function OrderListPage() {
  // value, modifier 함수를 반환
  const [orderList, setOrderList] = useRecoilState(orderList);

  const buyProduct = (product: IOrderList) => {
    // 새로운 배열을 return해야 함
    setToDos((oldOrderList) => [
      { product, id: Date.now(), category: "배송전" },
      ...oldOrderList,
    ]);
  };

  return (
    // JSX
  );
}

export default OrderListPage;

```



## 2. Selector

* derived state를 나타냄
  * derived state: state를 입력 받아 그것을 변형해 반환하는 순수함수를 거쳐 반환된 값을 말함
* 특정 조건의 state를 분류할 수 있음
* 다른 state를 만들 수 있음
* state를 원하는대로 변형
* atom의 output을 원하는대로 control



### get

* atom을 selector 내부에서 가져오는 함수

```typescript
import { atom, selector } from "recoil";

interface IOrderList {
  product: string;
  id: number;
  status: "배송전" | "배송중" | "배송완료";
}

// atom
export const orderList = atom<IOrderList[]>({
  key: "orderList",
  default: [],
});

export const selectedOrderStatus = atom<IOrderList["status"]>({
  key: "selectedOrderStatus",
  default: "배송전",
});

export const orderListSelector = selector({
  // selector의 key
  key: "orderListSelector",
  // get function
  // 인자로 options 객체를 받는데 get function이 들어있음
  get: ({ get }) => {
    // atom을 가져옴
    const orderList = get(orderList);
    const selectedOrderStatus = get(selectedOrderStatus);
    // 여기서 return하는 값이 이 selector의 value가 됨
    return [...orderList.filter((orderInfo) => orderInfo.status === selectedOrderStatus)];
  },
});

```



# Reference

[Nomad Coders - React JS 마스터클래스](https://nomadcoders.co/react-masterclass/lobby)

[Recoil Docs](https://recoiljs.org/ko/)

