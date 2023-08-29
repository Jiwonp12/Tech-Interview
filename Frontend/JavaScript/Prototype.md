# [JavaScript] Prototype

- 프로토타입이란 모든 객체들의 프로토타입 객체를 참조하는 숨겨진 링크를 말합니다.
- 프로토타입 객체는 처음 객체가 new 연산자를 통해 만들어진 다른 객체의 원형이 되는 객체를 말합니다.

## 프로토타입 객체

---

```jsx
function Person() {}

let kingjinsol = new Person();
let bee = new Person();

Person.prototype.getType = function () { // 프로토타입 객체 추가
	return '인간';
};

console.log(kingjinsol.getType()); // 인간
console.log(bee.getType()); // 인간
```

프로토타입 객체에 getType()이라는 함수를 추가하면 함수를 추가하기 전에 생성된 객체에서도 추가된 함수를 사용할 수 있습니다. 같은 프로토타입을 이용하여 생성된 kingjinsol과 bee 객체는 getType()을 사용할 수 있습니다.
주의할 점은 프로토타입 객체에 함수를 추가, 수정, 삭제할 때는 함수 안의 prototype 속성을 사용해야 합니다. 하지만 프로토타입 함수를 읽을 때는 함수 안의 prototype 속성 또는 객체 이름으로 접근합니다.

```jsx
bee.getType = function () { // bee 객체의 getType() 리턴 값을 곤충으로 수정
	return '곤충';
};

console.log(kingjinsol.getType()); // 인간
console.log(bee.getType()); // 곤충

bee.age = 29;

console.log(kingjinsol.age); // undefined
console.log(bee.age); // 29
```

여기서 주의해야 할 점은 생성된 객체의 함수를 수정할 때 prototype 속성을 사용하지 않고 객체의 함수를 수정하게 되면 프로토타입 객체에 있는 함수를 수정하는 것이 아니라 자신의 객체에 함수를 추가하는 것입니다.
이제 bee 객체를 사용하여 getType()을 호출하면 프로토타입 객체의 getType()을 호출한 것이 아니라 자신의 객체의 getType()을 호출한 것입니다.
프로토타입 객체의 함수를 수정할 경우에는 prototype 속성을 이용하여 수정합니다.

```jsx
Person.prototype.getType = function () {
	return '곤충';
}

console.log(kingjinsol.getType()); // 곤충
```

결론적으로 프로토타입 객체는 새로운 객체가 생성되기 위한 원형이 되는 객체입니다. 같은 원형으로 생성된 객체가 공통으로 참조하는 공간입니다.
프로토타입 객체의 함수를 읽는 경우에는 객체 또는 함수의 prototype 속성을 통해 접근할 수 있습니다. 하지만 추가, 수정, 삭제는 함수의 prototype 속성을 통해 접근해야 합니다.

## 프로토타입이란?

---

JavaScript에서는 객체가 만들어지기 위해서는 자신을 만드는 데 사용된 원형인 프로토타입 객체를 이용하여 객체를 만듭니다. 이때 만들어진 객체 안에 __proto__ 속성이 자신을 만들어낸 원형을 의미하는 프로토타입 객체를 참조하는 숨겨진 링크가 있습니다. 이 숨겨진 링크를 프로토타입이라고 정의합니다.

```jsx
function Person() {}
let jjinsol = new Person();
```

여기서 jjinsol 객체의 함수인 __proto__ 속성이 프로토타입 객체를 가리키는 숨은 링크를 프로토타입이라고 합니다.
프로토타입은 크게 두 가지로 해석됩니다. 함수의 멤버인 prototype 속성은 프로토타입 객체를 참조하는 속성입니다. 그리고 함수와 new 연산자가 만나 생성한 객체의 프로토타입 객체를 지정해주는 역할을 합니다. 객체 안의 __proto__ 속성은 자신을 만들어낸 원형인 프로토타입 객체를 참조하는 숨겨진 링크입니다.
JavaScript에서는 숨겨진 링크가 있어 프로토타입 객체 멤버에 접근할 수 있습니다. 그래서 이 프로토타입 링크를 사용자가 정의한 객체에 링크가 참조되도록 설정하면 코드의 재사용과 객체 지향적인 프로그래밍을 할 수 있습니다.

## 코드 재사용(상속)

---

JavaScript는 프로토타입 기반 언어입니다. 다른 클래스 기반 언어처럼 클래스를 이용한 상속을 할 수 없습니다. 그래서 JavaScript는 프로토타입을 이용해 코드 재사용을 할 수 있습니다.
JavaScript에서 코드 재사용은 크게 두 가지로 분류됩니다. classical 방식과 prototypal 방식으로 분류됩니다.
classical 방식은 new 연산자를 통해 생성한 객체를 사용하여 코드를 재사용하는 방법입니다. 마치 Java에서 객체를 생성하는 방법과 유사해 classical 방식이라고 합니다.
prototypal 방식은 리터럴 또는 Object.create()를 이용하여 객체를 생성하고 확장해 가는 방식입니다.
두 가지 방법 중 JavaScript는 prototypal 방식을 더 선호합니다. 그 이유는 classical 방식보다 간결하게 구현할 수 있기 때문입니다.

```jsx
// classical 방식
function Person(name) {
	this.name = name || '진솔';
}

Person.prototype.getName = function() {
	return this.name;
}

function Korean(name) {}
Korean.prototype = new Person();

let jinsol1 = new Korean();
console.log(jinsol1.getName()); // 진솔

let jinsol2 = new Korean('킹진솔');
console.log(jinsol2.getName()); // 진솔 -> Korean의 프로토타입이 이미 진솔로 정해져있음

// prototypal 방식
let person = {
	type: '인간',
	getType: function() {
		return this.type;
	},
	getName: function () {
		return this.name;
	}
};

let jinsol = Object.create(person);
jinsol.name = '진솔';

console.log(jinsol.getType()); // 인간
console.log(jinsol.getName()); // 진솔
```