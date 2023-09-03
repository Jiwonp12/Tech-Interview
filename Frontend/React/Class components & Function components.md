# 요약

1. 함수형 컴포넌트 + Hook을 사용하는 추세이다.

# 설명

## React 컴포넌트의 역할

리액트에서는 화면에 보이는 인터페이스를 설계할 때 ‘컴포넌트’ 단위로 설계가 이루어진다. 컴포넌트는 선언 방식에 따라서 함수형 컴포넌트, 클래스형 컴포넌트로 나눠진다.

## 함수형(Function) 컴포넌트

자바스크립트의 함수 형태로 표현되는 컴포넌트이다.

return 뒤에 JSX 코드를 넣어줘서 반환을 하게 된다.

```jsx
function about() {
  return (
    <div>
      <h2>Hello React</h2>
    </div>
  );
}

export default about;
```

자바스크립트에 익숙한 개발자라면 확실히 직관적이며, 메모리 지원도 클래스형 컴포넌트보다 덜 사용하게 된다. 빌드 후 배포할 때도 함수형 컴포넌트가 파일크기도 더 작아진다.

## 클래스형(Class) 컴포넌트

```jsx
import React, { Component } from "react";

class about extends Component {
  render() {
    return <div> Hello, React</div>;
  }
}

export default about;
```

위와 동일한 동작을 하는 코드를 클래스형 컴포넌트 형태로 변경시켰다. 클래스형 컴포넌트를 사용하려면 React에서 Component를 상속해서 만들어줘야 한다. 클래스형 컴포넌트에서는 **render** 라는 메서드를 이용해서 **JSX를 반환 시켜줘야 한다**. 클래스형 컴포넌트에서는 함수형 컴포넌트와는 다르게 LifeCycle과 State를 사용할 수 있다. 하지만 React Conf 2018에서 Sophie Aplert와 Dan Abramov가 Hook을 소개하면서 **React 16.8.0 버전 부터는 Hook을 지원하고, 공식 홈페이지에서 함수 컴포넌트를 사용하길 권장**한다.

**Class의 추가 기능들을 함수 컴포넌트 Hook을 통해서 모두 구현할 수 있다.**

그렇다면 Class 컴포넌트는 배울 필요가 없지 않을까? 생각할 수 있지만 꼭 그렇지도 않다. 현재 Class를 이용해서 만들고 현재까지 유지보수 되고 있는 수 많은 코드들이 존재한다. 그러한 프로그램들을 Hook으로 리뉴얼 시키기에는 큰 어려움이 있고, 버릴수는 없기 때문에 **유지보수를 위해서라도 Class 개념은 숙지하는 것이 필요하다.**

## 일반적인 차이점

**클래스형 컴포넌트**

- State와 LifeCycle API의 사용이 가능하다.
- 임의 메서드를 정의할 수 있다.

**함수형 컴포넌트**

- State와 LifeCycle API의 사용이 가능하다. (16.8 버전이후 제공되는 Hook으로 해결 가능)
- 클래스형 컴포넌트보다 선언하기 훨씬 편하다.
- 메모리 자원을 클래스형 컴포넌트보다 덜 사용한다.
- 빌드한 결과물의 크기 역시 클래스형 컴포넌트보다 작다.

## 선언방식의 차이점

**클래스형 컴포넌트**

- Class 키워드가 필요하며, 컴포넌트를 상속받아야 한다.
- 화면에 표시하기 위한 render() 메서드가 반드시 필요하다.

**함수형 컴포넌트**

- 클래스형 컴포넌트와 비교해서 훨씬 간결하게 코드를 작성할 수 있다.
- 함수 자체가 렌더 함수이기 때문에 render() 메서드를 사용하지 않아도 되고, 컴포넌트를 상속받지 않아도 된다.

## State 사용 차이

**클래스형 컴포넌트**

- constructor 안에서 this.state를 통해 초기 값을 설정 가능하며, constructor 없이도 초기 값을 설정할 수 있다. 또한 클래스형 컴포넌트의 state는 객체 형식이다.

```jsx
constructor(props){
	super(props);

	this.state = {
		name: 'soopiri'.
		items: []
	};
}
// without constructor
class App extents Component {
	state = {
		name: 'soopiri',
		items: []
	}
}
```

this.setState 함수로 state의 값을 변경할 수 있다.

```jsx
onClick={() => {
	this.setState({ price: price + 100 });
}}
```

**함수형 컴포넌트**

- useState로 state를 핸들링 한다. useState 함수를 호출하면 배열이 반환 되는데 첫 번째 원소는 state, 두 번째 원소는 setState의 역할을 하는 함수이며, useState의 파라미터는 state의 초기 값이다.

```jsx
const App = () => {
	const [name, setName] = useState('soopiri');

	const onButtonClick = {() => {
		setName('HAHA');
	}}
}
```

## Props 사용 차이

**클래스형 컴포넌트**

- this.props로 불러온다.

**함수형 컴포넌트**

- 렌더 함수의 parameter로 props를 전달받아 사용한다.

## LifeCycle 차이

모든 리액트 컴포넌트에는 라이프사이클이 있다. 컴포넌트는 생성(mount), 업데이트(update), 제거(unmount)의 생명주기를 갖는다. 적절한 생명주기에 어떤 작업을 처리해야 하는지 지정해줘야 불필요한 업데이트를 방지할 수 있다. 클래스형 컴포넌트에서는 LifeCycle API를 사용하며, 함수형 컴포넌트에서는 Hook을 사용한다.

**클래스형 컴포넌트**

- LifeCycle API는 컴포넌트가 DOM 위에 생성되기 전과 후의 데이터가 변경되어, 상태를 업데이트하기 전과 후로 실행되는 메서드 들이다.

**함수형 컴포넌트**

- 리액트 Hook은 함수형 컴포넌트에서 React State와 생명주기 기능을 연동(hook into) 할 수 있게 해주는 함수들이다. 클래스형 컴포넌트에서는 동작하지 않으며, Class 없이 React를 사용할 수 있게 해준다.

## 이벤트 핸들링

**클래스형 컴포넌트**

- 함수 선언 시 화살표 함수로 선언이 가능하며, 적용하기 위해선 this를 붙여야 한다.

```jsx
handleClick = e => {...}

render() {
	return (
		<>
			<input type='button' onClick={this.handleClick}>버튼</input>
		</>
	)
}
```

**함수형 컴포넌트**

- const 함수 형태로 선언해야 하며, this가 필요 없다.

```jsx
const handleClick = () => {...}

return (
	<>
		<input type='button' onClick={handleClick}>버튼</input>
	</>
)
```

# 예상질문

- 생명주기, LifeCycle API, Hook ?

# Ref

https://soopiri.tistory.com/23

https://react.vlpt.us/basic/24-class-component.html
