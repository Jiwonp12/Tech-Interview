# [JavaScript] 실행 컨텍스트와 Scope

- 실행 컨텍스트란 실행할 코드에 제공할 환경 정보들을 모아놓은 객체를 말합니다.
- 실행 컨텍스트가 활성화되면 호이스팅이 발생하고 외부 환경 정보를 구성합니다.
- 이 현상으로 인해 다른 언어에서 발견할 수 없는 특이한 현상들이 발생합니다.

## 실행 컨텍스트 구성



실행 컨텍스트는 다음과 같은 것들을 이용하면 call stack에 쌓이게 됩니다.

- `전역공간`
- `함수`를 실행
- `eval()` 함수 실행
- `block`을 만듦

일반적으로 함수를 이용한 실행 컨텍스트를 사용합니다.

```jsx
// var
var a = 1; // 전역 컨텍스트
function outer() { // outer 컨텍스트
	function inner() { // inner 컨텍스트
		console.log(a); // undefined
		var a = 3;
		console.log(a); // 3
	};
	inner();
	console.log(a); // 1
};
outer();
console.log(a); // 1

// let -> 에러? TDZ(일시적 사각지대) 구간에 빠지는 것 같음.
// inner 스코프 내에서 a의 선언이 있기 때문에 전역에 있는 a를 참조하지 못함
// 스코프의 시작 지점부터 초기화 시작 지점까지의 구간을 TDZ(Temporal Dead Zone)라고합니다.
let a = 1;
function outer() { // outer 컨텍스트
	function inner() { // inner 컨텍스트
		console.log(a);
		let a = 3;
		console.log(a);
	};
	inner();
	console.log(a);
};
outer();
console.log(a);
```

위의 코드를 실행했을 때 실행 컨텍스트의 스택은 다음과 같은 순서로 실행됩니다.

- 프로그램 실행: `[전역 컨텍스트]`
- outer 실행: `[전역 컨텍스트, outer]`
- inner 실행: `[전역 컨텍스트, outer, inner]`
- inner 종료: `[전역 컨텍스트, outer]`
- outer 종료: `[전역 컨텍스트]`

그리고 이러한 실행 컨텍스트를 구성할 때 생기는 것들이 있습니다.

- `VariableEnvironment`
    - 현재 컨텍스트 내의 식별자(변수)들에 대한 정보
    - 외부 환경 정보
    - 선언 시점의 LexicalEnvironment의 스냅샷(변경사항 반영 X)
- `LexicalEnvironment`
    - 처음에는 VariableEnvironment와 같음
    - 변경 사항이 실시간으로 반영됨
- `ThisBinding`
    - 식별자가 바라봐야할 대상의 객체

> **Variable Environment**
> 

VariableEnvironment에 담기는 내용은 LexicalEnvironment와 같지만, 최초 실행 시의 스냅샷을 유지합니다. 실행 컨텍스트를 생성할 때 VariabeEnvironment에 정보를 먼저 담은 다음, 이를 복사해서 LexicalEnvironment를 만듭니다.

주로 활용하는 것은 LexicalEnvironment입니다. 즉, VariableEnvironment는 스냅샷 유지를 목적으로 사용합니다.

> **Lexical Environment**
> 

LexicalEnvironment의 내부에는 environmentRecord와 outerEnvironmentReference로 구성되어 있습니다.

- environmentRecord로 인하여 호이스팅이 발생합니다.
- outerEnvironmentReference로 인하여 스코프와 스코프 체인이 형성됩니다.

## environmentRecord와 Hoisting(호이스팅)



JavaScript 코드는 실행하기 전에 식별자를 수집합니다.

> environmentRecord
> 

현재 컨텍스트와 관련된 코드의 식별자 정보들이 저장됩니다.

- 매개변수 식별자
- 함수 자체
- 함수 내부의 식별자

> Host Object(호스트 객체)
> 
- 전역 실행 컨텍스트는 변수 객체를 생성하는 대신 전역 객체를 활용합니다.
- 브라우저의 Window 객체, Node의 Global 객체 등이 이에 해당합니다.
- 이들은 Host Object로 분류됩니다.

즉 코드가 실행되기 전에 JavaScript 엔진은 이미 실행 컨텍스트에 속한 변수명들을 모두 알고 있게 되는 셈입니다.

이때 호이스팅이라는 개념이 이용됩니다.

“*JavaScript 엔진은 식별자들을 최상단으로 끌어올려놓은 다음 실제 코드를 실행한다.”*라고 생각해도 코드 해석에 문제되는 것이 없습니다.

중요한 점은, JavaScript 엔진이 실제로 변수를 끌어올리지는 않지만, 편의상 끌어올리는 것으로 간주하자는 것입니다.

```jsx
function a () {
  var x = 1;
  console.log(x);
  var x ;
  console.log(x);
  var x = 2;
  console.log(x);
}
a();
```

위의 코드는 다음과 같이 해석될 수 있습니다.

```jsx
function a () {
  var x;
  var x;
  var x;

  x = 1;
  console.log(x); // 1
  console.log(x); // 1
  x = 2;
  console.log(x); // 2
}
a();
```

변수의 호이스팅은 이처럼 해석될 수 있습니다. 그러나 함수의 호이스팅은 조금 다릅니다.

```jsx
function a() {
  console.log(b);
  var b = 'bbb';
  console.log(b);
  function b() {};
  console.log(b);
}
a();
```

변수의 경우 정의하는 부분만 호이스팅이 발생하지만, 함수는 함수 전체가 호이스팅이 됩니다.

```jsx
function a() {
	var b;
	function b() {};
	console.log(b); // f b() {}
	b = 'bbb';
	console.log(b); // bbb
	console.log(b); // bbb
}
a();
```

## outerEnvironmentReference와 Scope



> **Scope**
> 

스코프란 식별자에 대한 유효범위입니다.

- Scope A의 외부에서 선언한 변수는, A의 외부/내부 모두 접근 가능합니다.
- A의 내부에서 선언한 변수는 오직 A의 내부에서만 접근할 수 있습니다.

스코프의 개념은 대부분의 언어에 존재하지만, ES5까지의 JavaScript는 특이하게도 오직 함수에 의해서만 스코프가 생성됩니다.

> **Scope Chain**
> 
- 식별자의 유효범위를 안에서 바깥으로 차례로 검색해 나가는 것입니다.
- 이를 가능하게 하는 것이 outerEnvironmentReference입니다.

outerEnvironmentReference는 현재 호출된 함수가 선언될 당시의 LexicalEnvironment를 참조합니다.

`선언하다`라는 행위가 실제로 일어날 수 있는 시점은 콜 스택 상에서 어떤 실행 컨텍스트가 활성화된 상태일 때 뿐입니다. 모든 코드는 실행 컨텍스트가 활성화 상태일 때 실행되기 때문입니다.

```jsx
var a = 1; // 전역 컨텍스트
function outer () { // outer 컨텍스트
  function inner () { // inner 컨텍스트
    console.log(a);
    var a = 3;
    console.log(a);
  }
  inner(); // inner가 실행될 때 outer의 LexcicalEnvironemnt를 outerEnvironmentReference로 참조한다.
  console.log(a);
}
outer(); // outer가 실행될 때 전역 컨텍스트의 LexcicalEnvironemnt를 outerEnvironmentReference로 참조한다.
console.log(a);
// 위의 코드는 다음과 같은 scope chain을 형성합니다.
inner LexicalEnvironment {
	식별자 a
	outerEnvironmentReference = outer LexicalEnvironment {
		식별자 a
		outerEnvironmentReference = global LexicalEnvironment {
			식별자 a
		}
	}
}
```

이러한 구조적 특성 때문에 여러 스코프에 동일한 식별자를 선언할 경우, 무조건 scope chain 상에서 가장 먼저 발견된 식별자에만 접근 가능하게 됩니다.

```jsx
inner LexicalEnvironment {
	식별자 a  // inner function에서 a에 접근할 때 여기에 가장 먼저 접근
	outerEnvironmentReference = outer LexicalEnvironment {
		식별자 a  // outer function에서 a에 접근할 때 여기에 가장 먼저 접근
		식별자 b  // inner function에서 b에 접근할 때 여기에 가장 먼저 접근
		outerEnvironmentReference = global LexicalEnvironment {
			식별자 a  // 전역에서 a에 접근할 때 여기에 가장 먼저 접근
      식별자 b  // 전역에서 b에 접근할 때 여기에 가장 먼저 접근
      식별자 c  // inner function에서 c에 접근할 때 여기에 가장 먼저 접근
		}
	}
}
```