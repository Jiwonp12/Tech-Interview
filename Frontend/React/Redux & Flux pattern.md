# 요약

1. MVC 패턴의 한계로 Flux 패턴이 등장했다.
2. Flux 패턴은 단방향 데이터 흐름이다.
3. Redux는 1개의 store를 갖고, store를 변경하는 reducer를 여러 개 가진다.
4. 프로젝트 규모에 맞게 Redux의 도입 여부를 결정하는 것을 권장한다.

# 설명

## Flux 패턴이 등장한 이유

React는 Single Page App, 하나의 페이지로 앱을 다루는 경우가 많은데, 규모가 커질수록 단 하나의 Controller로 여러가지 View와 Model을 관리하면 깔끔해지기 어렵다. 그리고 한 View에서 일어난 상호작용 때문에 여러 Model이 변경되거나, 그 반대의 일도 벌어지기 때문에 코드를 이해하기도 어렵다. 따라서 페이스북은 이렇게 데이터가 중구난방으로 전달되는 상황을 줄이고 보다 깔끔하게 만들고자 Flux 패턴을 만들어낸다.

## Flux 패턴이란

어디서 어느 방향으로 데이터가 전달될지 못할 정도로 혼란한 MVC 패턴의 복잡성을 해소하기 위해, Flux 패턴에서는 데이터가 한 방향으로만 흐르도록 했다. Action → Dispatcher → Store → View 가 기본적인 Flux의 형태로, 어떤 Action이 발생하면, Dispatcher에서 이를 받아와 해석한 후 Store에서 저장된 정보에 변경을 가하고, 그 결과가 View로 다시 전달되도록 한다.

그런데 모바일에서 터치를 하는 것처럼, 웹에서도 사용자가 View를 통해서 클릭 같은 액션을 발생시킬 수 있다. 그런 경우에 Dispatcher와 View 사이에 Action이 추가된 흐름이 만들어진다.

어디에서든 Action이 발생하면, Dispatcher를 통해 **단방향**으로 흘러간다고 이해하면 될 것 같다.

## Redux

Redux는 Dan Abramov라는 개발자가 Flux 패턴과 Reducer를 결합하여 만든 상태 관리 라이브러리이다. Redux를 사용하면 State 관리 로직을 컴포넌트와 분리시킴으로써 효율적으로 관리할 수 있게 되며, 컴포넌트 끼리 State를 공유할 때 여러 컴포넌트를 거쳐 props를 복잡하게 전달(Props Drilling)하지 않아도 손쉽게 값을 전달할 수 있게 된다.

## Redux의 동작 원리

Redux는 Store라는 전역 상태 저장소를 통해 State와 Reducer를 저장한다. Redux는 애플리케이션 하나 당 하나의 Store만을 생성하며, 유용한 몇 가지 내장 함수를 같이 제공한다. 각 컴포넌트들은 이러한 내장 함수들을 사용하여 Store의 데이터에 접근하고 변경을 요청할 수 있다.

Store를 변경하기 위한 로직을 저장하는 곳이 바로 Reducer이다. Reducer는 Flux 패턴에는 없는 Redux만의 고유한 개념으로 현재 State와 Action을 인수로 전달 받아 Store에 접근하고, 전달 받은 Action을 참고하여 새로운 State를 만들어 반환한다.

이러한 Reducer를 원하는 조건에 따라 호출하는 것이 바로 Action이다. State에 어떠한 변화가 필요할 때 Action을 발생시킴으로써(Dispatch) Reducer에 전달한다.

마지막으로 Dispatch와 함께 Store의 내장 함수 중 하나인 Subscribe을 통해 Action이 Dispatch될 때마다 인수로 전달한 함수를 호출하도록 설정할 수 있다.

Redux에서 State를 관리하는 작업의 흐름은 다음과 같이 진행된다.

1. 사용자가 UI를 통해 컴포넌트 내에 존재하는 이벤트를 호출함.
2. 이벤트와 연결된 액션 생성 함수(Action Creator)가 호출됨.
3. 액션 생성 함수에서 생성된 Action이 호출됨.
4. 호출된 Action이 Reducer로 전달(Dispatch)됨.
5. Reducer에서 Dispatch된 Action에 따라 State값을 변경.
6. 변경된 State가 렌더링되어 UI에 표시됨.

## Redux의 세 가지 원칙

Redux에서는 반드시 준수해야 하는 세 가지 원칙이 있다.

1. 하나의 애플리케이션 안에는 하나의 Stroe만 사용해야 한다. 이렇게 함으로 서버로부터 가져온 State가 직렬화(Serialization)된 채 전달될 수 있으며, 클라이언트 측에서는 이를 추가적인 코드 없이 곧바로 사용할 수 있다.
2. State는 읽기 전용이다. State를 변화 시키는 유일한 방법은 Action을 전달하는 것 뿐이다. 이를 통해 모든 State 변화를 중앙에서 관리할 수 있으며, 변경에 대한 추적이 용이해 진다.
3. State의 변화를 일으키는 Reducer는 순수 함수로 작성되어야 한다. Reducer는 현재 State와 Action을 전달 받아 다음 State를 반환하는 순수 함수이다. 즉, 이전 State를 변경하는 것이 아니라 새로운 State 객체를 생성하여 반환하는 것임을 잊지 말아야 한다.

## Redux의 필요성

Redux를 사용하면 전역 상태 관리를 매우 효과적으로 수행할 수 있게 된다. 하지만 이러한 전역 상태 관리는 MobeX, Recoil, Zotai등 다른 상태 관리 라이브러리를 대신 사용할 수도 있으며, React의 Context API를 통해서도 충분히 동일한 작업을 수행할 수 있다. 또한, Redux를 사용하게 되면 단 하나의 State를 바꾸기 위해 요청을 전달하는 Action과 상태를 바꿔주는 Redux를 생성해야 하는 등 추가적인 코드의 양이 늘어나게 된다. 따라서 반드시 Redux를 사용하는 것이 아닌 해당 프로젝트의 특징과 확장성 등을 고려하여 Redux의 도입 여부를 결정하는 것을 권장한다.

# 예상질문

- Redux를 사용하는 이유?
- Redux의 장단점에 대해 설명해주세요
- Context API와 Redux를 비교해주세요
- Redux Thunk, Redux Saga에 대해 설명해주세요

# Ref

[https://medium.com/hcleedev/web-react-flux-패턴-88d6caa13b5b](https://medium.com/hcleedev/web-react-flux-%ED%8C%A8%ED%84%B4-88d6caa13b5b)

https://www.tcpschool.com/react/react_redux_intro

[https://velog.io/@wns450/기술면접-Redux-7](https://velog.io/@wns450/%EA%B8%B0%EC%88%A0%EB%A9%B4%EC%A0%91-Redux-7)
