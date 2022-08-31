# Recoil & Custom Hook & styled-components를 활용한 전역 모달 구현

## 1. 서론

Modal이란, 주 창에 종속된 그래픽 인터페이스이다. 보통 사용자의 입력에 따른 피드백, 오류, 안내 등을 나타내기 위한 목적으로 사용한다. 이번에 진행하는 프로젝트에서도 이런 목적의 모달들이 기획이 되었다. 설계 단계부터 내가 맡아서 만들게 되었으므로 구조부터 잡아가야했다.



### 어떻게 구현할지?

* 구현할 서비스에서 모달은 사용자의 입력에 따른 피드백, 오류, 안내 등을 나타내기 위한 목적으로 사용될 것
  * 이외에도 사용자의 입력을 받는 모달도 구현되어야 함
* 구현할 모달을 카테고리화
  * Alert Modal: 사용자에게 오류/안내를 나타내는 모달, Template화 필요
  * Custom Modal: 특정 페이지에서만 독립적으로 사용될 모달, Template화 필요 없음
  * why? Alert Modal은 페이지 어디에서든 띄울 수 있어야 하므로 Template화 하여 불러내야한다. 반면, Custom Modal은 특정 페이지에서만 종속적으로 사용될 것이기 때문에 굳이 Template화 할 필요는 없다. 한 Custom Modal이 두 페이지에서 사용되어야한다면, 그 때 Template화 하면 된다.
* **전역적으로 관리되어야 함**
  * Recoil: 로컬 전역 상태 관리
  * Custom Hook: 모달 관련 로직을 함수화하여 어느 컴포넌트에서 불러도 독립적으로 동작하도록 함
  * Global Modal: 루트에 가깝게 컴포넌트를 주입하여 (Layout 수준) 전역 모달 상태에 따라 띄워지도록 함
* 모달은 여러개가 뜰 수 있도록 할 것을 염두
  * 기존 서비스에서 프로모션 모달과 주의 모달이 같은 Redux state에서 관리되었었는데, 단 하나만 띄워지도록 로직이 구현되어 있었다. 때문에, 중요한 사항의 모달을 프로모션 모달이 가리게되어 유저가 볼 수 없는 경우가 발생하였다. 이를 방지하여, 여러개의 모달이 띄워질 수 있도록 설계한다.

![modal](/Users/jaeminjeon/Documents/Study/Programming/TIL/Project/images/modal.png)

## 2. Modals Atom

* App 내 띄워져야 할 모든 모달을 관리하는 atom

  **회사 비지니스 코드를 올릴 수는 없으므로 아주 간략하게 얼개만 알 수 있는 수준으로 올림에 양해 바람**



### atom.ts

* app내 띄워질 모달은 배열의 요소로 가지게 될 것

```TypeScript
import { atom } from 'recoil';
import IModalsInfoAtom from './interface';

const modalsInfoAtom = atom<IModalsInfoAtom>({
  key: 'modalsInfoAtom ',
  default: {
    modals: [],
  },
});

export default modalsInfoAtom;
```



### interface.ts

* Modal Atom의 interface 정의

```TypeScript
// 모달의 고유 ID
// 해당 ID를 기준으로 특정 모달만을 종료시키거나 찾을 수 있도록 함
type Id = `modal-${string}`;
// 모달의 아이콘 style
type Icon = 'check' | 'cross';

// alert modal에 대한 인터페이스
interface IAlertModalConfig {
  type: 'alert';
  text: JSX.Element;
  icon?: Icon;
  oneButton?: {
    text: string;
    func: () => void;
  };
  twoButtons?: {
    left: {
      text: string;
      func: () => void;
    };
    right: {
      text: string;
      func: () => void;
    };
  };
  autoExecution?: () => void;
}

interface ICustomModalConfig {
  type: 'custom';
  elements: JSX.Element;
}
interface IModalInfo {
  id: Id;
  config: IAlertModalConfig | ICustomModalConfig;
}

interface IModalsInfoAtom {
  modals: IModalInfo[];
}

export default IModalsInfoAtom;

export { IModalInfo, IAlertModalConfig, ICustomModalConfig };
```



### selector.ts

* Modal Atom을 기준으로 파생 상태를 나타내거나 새로운 상태를 넣는 selector

```TypeScript
import { DefaultValue, selector } from 'recoil';
import { IModalInfo } from './interface';
import modalsInfoAtom from './atom';

// 노출할 modal을 가져오거나 modal 배열을 변경
const modalsSelector = selector<IModalInfo[]>({
  key: 'modalsSelector',
  get: ({ get }) => {
    const { modals } = get(modalsInfoAtom);
    return modals;
  },
  set: ({ get, set }, newValue) => {
    if (newValue instanceof DefaultValue) return;
    const newModals = newValue;
    const newMoalsInfoAtom = {
      ...get(modalsInfoAtom),
      modals: newModals,
    };
    set(modalsInfoAtom, newMoalsInfoAtom);
  },
});

// 현재 노출할 모달 배열을 기준으로 app 내 노출할 모달이 있는지 없는지에 대한 값을 return
const isShowModalSelector = selector<boolean>({
  key: 'isShowModalSelector',
  get: ({ get }) => {
    const {
      modals: { length },
    } = get(modalsInfoAtom);
    const isShowModal = length > 0;
    return isShowModal;
  },
});

export { modalsSelector, isShowModalSelector };
```



## 3. useModal.ts

* 모달 관련 로직을 함수화한 Hook
* 어느 컴포넌트에서나 불러와서 사용 가능
  * 독립적인 동작 보장(함수 이므로)

```React
import { useCallback } from 'react';
import { useRecoilState, useRecoilValue } from 'recoil';
import { modalsSelector, isShowModalSelector } from '../recoil/modals';
import { IModalInfo, IAlertModalConfig, ICustomModalConfig } from '../recoil/modals/interface';

type ModalId = IModalInfo['id'];

const useModal = (key?: string) => {
	// 해당 Hook이 호출 되면, 넘겨받은 key를 기준으로 모달 ID를 생성
  const modalId: ModalId = `modal-${key}`;
	// modal 노출 여부
  const isShowModal = useRecoilValue(isShowModalSelector);
  // 모달 배열 접근 또는 모달 배열 수정
  const [modals, setModals] = useRecoilState(modalsSelector);
	// alert modal을 생성하는 함수
  const createAlertModal = useCallback(
    (alertModalConfig: IAlertModalConfig) => {
      setModals((prevModals) => [
        ...prevModals,
        {
          id: modalId,
          config: { ...alertModalConfig },
        },
      ]);
    },
    [modalId, setModals],
  );
// custom modal을 생성하는 함수
  const createCustomModal = useCallback(
    (customModalConfig: ICustomModalConfig) => {
      setModals((prveModals) => [
        ...prveModals,
        {
          id: modalId,
          config: { ...customModalConfig },
        },
      ]);
    },
    [modalId, setModals],
  );
// 모달을 닫는 함수
// 해당 Hook에서 생성된 모달만을 종료
  const closeModal = useCallback(() => {
    setModals((prevModals) => {
      return prevModals.filter(({ id }) => id !== modalId);
    });
  }, [modalId, setModals]);
  const closeAllModal = () => {
    setModals([]);
  };

  return {
    isShowModal,
    modals,
    createAlertModal,
    createCustomModal,
    closeModal,
    closeAllModal,
  };
};

export default useModal;
```



## 4. GlobalModal.tsx

* 전역 모달 컴포넌트
* Modal Atom을 가져와서 띄움

```React
import React from 'react';
import styled from 'styled-components';
import { useModal } from './hooks';
import { IModalInfo } from './recoil/modals/interface';
import AlertModal from './AlertModal';

const OverLay = styled.div`
  position: absolute;
  z-index: -1;
  display: flex;
  justify-content: center;
  align-items: center;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: ${(props) => props.theme.effects.modalDim};
`;

interface IRenderModalProps {
  modalInfo: IModalInfo;
}

// 모달의 타입에 따라서 분기처리하여 렌더링
function RenderModal({ modalInfo }: IRenderModalProps) {
  const { config } = modalInfo;
  const { type } = config;
  switch (type) {
    case 'alert':
      return <AlertModal config={config} />;
    case 'custom':
      return config.elements;
    default:
      return null;
  }
}

function GlobalModal() {
  const { isShowModal, modals } = useModal();

  if (!isShowModal) {
    return null;
  }

  return (
    <OverLay>
			{/* modal atom의 modals에 접근하여 map으로 modal을 렌더링(복수 modal 허용) */}
      {modals.map((modalInfo) => (
        <RenderModal key={modalInfo.id} modalInfo={modalInfo} />
      ))}
    </OverLay>
  );
}

export default GlobalModal;
```





## 4. 느낀점

프로젝트를 하면서 가장 재밌었던 작업이었다. 도입한 다양한 라이브러리들의 적절한 기능을 활용할 수 있었다. 모든 모달의 로직을 Custom Hook에 정의하여  필요한 곳에서 내부 로직을 신경쓰지 않고 모달 기능을 사용할 수 있도록 하였다. Custom Hook이 왜 유용한지 조금이나마 와닿게 느낄 수 있었다.



## 5. 참고 문헌

* [모달이란?](https://namu.wiki/w/%EB%AA%A8%EB%8B%AC%20%EC%B0%BD)
* [Recoil과 hook으로 global 모달 만들기](https://dev.to/leoarada/recoil-hook-global-514)
* [dialog 요소가 가진 슈퍼 파워 알아보기](https://ui.toast.com/posts/ko_20220518)
* [4 steps to set up global modals in React](https://opensource.com/article/21/5/global-modals-react)

