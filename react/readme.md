# React

## React가 만들어진 이유
- 2010년대에 Facebook(현 Meta)은 SPA(Single Page Application)인 페이스북에 타임라인, 채팅, 친구 목록, 게임 등 많은 기능을 넣고자 했는데, 전통적인 웹 기술로는 이를 구현하기 너무 복잡하고 어려웠다.
- 이러한 문제를 해결하기 위해, 개발자가 웹 애플리케이션에서 빠르고 효율적으로 사용자 인터페이스를 구현하기 쉽도록 Facebook(현 Meta)에서 만든 라이브러리가 React이다.

## Virtual DOM
- Virtual DOM은 DOM의 구조를 메모리 상에서 구현한, React의 특성 중 하나이다.
- React는 상태의 변화에 반응하여 DOM을 갱신하는데, 이 때 DOM을 갱신하는 작업은 비용이 매우 큰 작업이므로, 상태가 변화했을 때 Virtual DOM을 먼저 갱신한 뒤, 갱신된 부분만을 조사하여 목록으로 만든 다음, 해당하는 부분만 실제 DOM으로 반영한다.
- React는 이러한 방식으로 DOM을 효율적으로 갱신한다.

## JSX
- JavaScript에서 마크업 형태의 코드를 작성할 수 있게 해주는 JavaScript 문법의 확장이다.
- React의 클래스 컴포넌트의 render 메소드나 함수형 컴포넌트의 return문에 주로 HTML처럼 보이는 코드를 작성하게 되는데, 이를 컴파일할 때 React.createElement로 변환된다.

## key
- key는 React에서 배열같은 Collection 타입을 렌더링할 때 엘리먼트와 데이터 사이의 관계를 추적함에 있어 필수적인 Prop이다.
- key가 제대로 입력되지 않으면, Collection에 item의 추가/변경/삭제가 있을 때, 예상하지 못한 동작으로 이어질 수 있다.
- 그 외에도, Props나 State에 변화가 없음에도 컴포넌트의 재렌더링이 필요할 때, 새로운 key를 제공하는 방법을 통해 갱신할 수도 있다.

## State와 Props의 차이
- State는 컴포넌트 자기 자신이 갖고 있는 값이다.
  - 컴포넌트 생명 주기동안 setState 등등을 통해 갱신할 수 있다.
  - 재렌더링 후에도 유지된다.
  - State 값의 갱신에 왜 setState를 사용하는가?
    - setState를 통해 새로운 값을 알려야 갱신을 할 수 있기 때문이다.
    - 직접 State를 변경할 경우, React에선 변경해야 하는지 여부를 알 수 없다.
- Props는 부모 컴포넌트에서 자식 컴포넌트로 전달되는 값이다.
  - 갱신할 수 없다.
  - 표시하거나 다른 값으로 활용될 때에 쓰인다.

## Prop Drilling
- 부모 컴포넌트에서 자식 컴포넌트에 Props를 전달할 때 자식 컴포넌트가 위계상으로 부모와 너무 멀리 떨어져 있으면, 그 사이에 있는 컴포넌트들이 Props가 필요하지 않아도 오로지 최종 목적지 자식 컴포넌트를 위해서 불필요하게 Props를 전달하게 되는 상황을 말한다.
- 이는 해당 자식 컴포넌트를 변경해야 할 때 원치 않는 다른 컴포넌트까지 전부 변경해야 하므로 유지보수에 어려움을 초래한다.
- 꾸준한 리팩토링으로 Props 전달까지 거리를 줄이거나, Context API 또는 상태 관리 라이브러리를 통해 Prop Drilling을 최소화할 수 있다.

## Context API
- Prop Drilling을 해결하기 위해, 컨텍스트 내에 있는 컴포넌트들이 컨텍스트에 있는 값을 읽어올 수 있도록 만든 React의 API이다.

## 상태 관리 라이브러리
- 어느 때에 상태 관리 라이브러리를 사용할까?
  - 상태가 자주 바뀐다.
  - Prop Drilling같은 부적절한 현상이 자주 일어난다.
  - 앱의 최상단 컴포넌트가 앱의 모든 상태를 가지는 것이 더 이상 부적절하다.
- 예시: Redux, MobX, Tanstack Query (React Query), Zustand 등등

## 훅
- 함수형 컴포넌트의 생명 주기 동안 활용할 수 있는 함수.
- 생명 주기 함수 등, 클래스 컴포넌트의 장점을 함수형 컴포넌트에서 활용하려는 시도라고 볼 수 있다.
- React 16부터 함수형 컴포넌트에 새로 추가된 기능이다.
- 장점
  - 클래스 컴포넌트, this, 클래스 컴포넌트 내 생명 주기 함수 등등을 사용할 필요가 없어진다.
  - 공통적인 기능을 커스텀 훅으로 만들어 재사용성 높은 로직을 작성하기 쉬워진다.
  - 컴포넌트 자체에서 분리되어 읽기 쉽고 테스트하기 용이한 코드를 작성할 수 있다.

### useState
- 컴포넌트 내의 상태를 관리하기 위한 훅.
- State 값이 setState를 통해 갱신될 때, 컴포넌트가 재렌더링된다.
- [State 값, setState 함수] 배열 형태로 반환된다.

### useEffect
- 컴포넌트가 렌더링된 뒤 전달받은 이펙트 콜백을 실행하는 훅.
- 의존성 배열에 관해
  - 의존성 배열이 아예 제공되지 않은 경우, 컴포넌트가 재렌더링될 때마다 이펙트 콜백을 실행한다.
  - 빈 의존성 배열이 제공된 경우, 컴포넌트가 생성될 때 딱 한 번만 이펙트 콜백이 실행된다.
  - 값이 들어있는 의존성 배열이 제공된 경우, 의존성 배열 내 값이 변경될 때마다 이펙트 콜백이 실행된다.
- 이펙트 콜백 내 return문에 있는 함수는 컴포넌트가 파괴될 때 실행하는 일급 함수이다.
- 사용 방법
  - [컴포넌트 자체에서 통제할 수 없는 부분, 즉 백엔드 API 호출같은 외부 시스템과의 연결이 필요할 경우 등에 사용할 수 있다.](https://ko.react.dev/reference/react/useEffect#connecting-to-an-external-system)
  - [React로 작성되지 않은 위젯을 제어할 때에도 사용할 수 있다.](https://ko.react.dev/reference/react/useEffect#controlling-a-non-react-widget)
- 왜 Effect라고 하는 걸까?
  - React의 함수형 컴포넌트는 최대한 순수 함수처럼 구성되어 있는데, 함수형 컴포넌트에서 API 호출이나 다른 부분을 갱신하는 등의 영향을 끼치기 위해선 이 훅을 사용해야 한다.
  - 이 때, 부수적인 효과(Side Effect)를 일으키는 것처럼 보인다고 Effect라고 이름지어진 것으로 알고 있다.

### useMemo
- 전달받은 콜백 함수의 리턴값을 Memoization함으로써 컴포넌트를 최적화할 수 있는 훅.
- 의존성 배열에 관해
  - 의존성 배열이 아예 제공되지 않은 경우, 컴포넌트가 재렌더링될 때마다 새로운 콜백 결과값이 제공된다.
  - 빈 의존성 배열이 제공된 경우, 컴포넌트가 생성될 때 딱 한 번만 새로운 콜백 결과값이 제공된다.
  - 값이 들어있는 의존성 배열이 제공된 경우, 의존성 배열 내 값이 변경될 때마다 새로운 콜백 결과값이 제공된다.
- 언제 쓰면 좋을까?
  - [재계산을 건너뛸 수 있기 때문에, Memoization하고자 하는 값이 복잡한 계산을 통해 생성된 경우, 즉 계산 비용이 높을수록 효과적이다.](https://ko.react.dev/reference/react/useMemo#skipping-expensive-recalculations)
  - [컴포넌트 재렌더링을 생략할 때에도 효과적이다.](https://ko.react.dev/reference/react/useMemo#skipping-re-rendering-of-components)

### useCallback
- 전달받은 함수를 캐싱함으로써 컴포넌트를 최적화 수 있는 훅.
- useMemo와 달리, useCallback은 전달받은 함수를 자체적으로 실행하지 않는다.
- 의존성 배열에 관해
  - 의존성 배열이 아예 제공되지 않은 경우, 컴포넌트가 재렌더링될 때마다 새로운 함수가 제공된다.
  - 빈 의존성 배열이 제공된 경우, 컴포넌트가 생성될 때 딱 한 번만 새로운 함수가 제공된다.
  - 값이 들어있는 의존성 배열이 제공된 경우, 의존성 배열 내 값이 변경될 때마다 새로운 함수가 제공된다.
- 언제 쓰면 좋을까?
  - [컴포넌트 재렌더링을 생략할 때 효과적이다.](https://ko.react.dev/reference/react/useCallback#skipping-re-rendering-of-components)

### useRef
- 렌더링에 필요하지 않은 값을 참조할 수 있게 해주는 훅.
- 언제 쓰면 좋을까?
  - 값이 갱신되어도 리렌더링이 되지 않길 원하는 경우 사용할 수 있다.
  - [focus나 blur나 스크롤 또는 비디오 재생 등, DOM을 직접 조작하고 싶을 때 사용할 수 있다.](https://ko.react.dev/reference/react/useRef#examples-dom)
- 특징
  - 마운트된 시점부터 언마운트될 때까지 값이 유지된다.
  - [current 속성은 변경을 해도 컴포넌트가 재렌더링되지 않는다.](https://ko.react.dev/reference/react/useRef#referencing-a-value-with-a-ref)