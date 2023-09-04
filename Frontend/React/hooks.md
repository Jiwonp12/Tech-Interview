### hooks은 무엇인가요?
Hooks는 클래스 기반 컴포넌트의 장점(예를 들어 내부 상태와 생명주기 메소드)을 함수형 컴포넌트로 가져오려는 리액트의 시도이다.
리액트 Hooks의 장점은 무엇인가요?
공통 기능을 커스텀 hook으로 로직 재사용 가능하며,컴포넌트 자체에서 로직을 분리할 수 있어서 읽기 쉽고 테스트하기 쉬운 코드를 작성할 수 있다. 함수 안에서 다른 함수를 호출하는 것으로 새로운 hook을 만들어 볼 수 있다. 기존의 class component는 여러 단계의 상속으로 인해 전반적으로 복잡성과 오류 가능성을 증가시켰다. 하지만 function component에 hooks에 도입되면서 class component가 가지고 있는 기능을 모두 사용할 수 있음은 물론이고 기존 class component 복잡성, 재사용성의 단점들까지 해결된다.
### 규칙
최상위에서만 호출해야한다. 리액트 함수 컴포넌트에서만 호출해야한다. 이 규칙을 강제하는 플러그인은 eslint-plugin-react-hooks 으로 create react app에 기본적으로 포함되어 있다.
훅이 개발자에게 도달되는 흐름은 다음과 같다.
reconciler -> shared/ReactSharedInternal -> react/ReactSharedInternal -> react/ReactCurrentDispatcher -> react/ReactHooks -> react -> 개발자
### 훅은 어떻게 생성되나요?
1. 훅 객체 생성
컴포넌트가 마운트 될 때 useState()를 호출할 경우 fiber의 memoizedState는 null이므로 mount 구현체인 mountState()를 사용하게 된다.
firstWorkInProgressHook은 훅 연결 리스트의 head로 renderWithHooks()에서 컴포넌트 실행이 끝났을 때 fiber에 저장되어 컴포넌트와 훅 리스트를 연결해주고 workInProgressHook은 현재 처리되고 있는 훅을 나타내면서 동시에 리스트의 tail 포인터로 사용한다.
2. update를 담을 queue 생성
훅을 이용하여 컴포넌트 상태를 변경하고자 할 때 업데이트 정보를 담고 있는 update 객체가 생성된다. 이 객체는 훅의 queue에 저장된다.

### 출처
https://goidle.github.io/react/in-depth-react-hooks_1/


