# 요약

1. this는 객체 자신의 프로퍼티나 메서드를 참조하기 위한 **자기 참조 변수**이다.
2. this가 가리키는 값, 즉 **this 바인딩은 함수 호출 방식에 따라 동적으로 결정**된다.

# 설명

| 함수 호출 방식       | this가 가리키는 값(this 바인딩)        |
| -------------------- | -------------------------------------- |
| 일반 함수로서 호출   | 전역 객체, strict mode = undefined     |
| 메서드로서 호출      | 메서드를 호출한 객체(마침표 앞의 객체) |
| 생성자 함수로서 호출 | 생성자 함수가 (미래에) 생성할 인스턴스 |

## 함수 호출 방식에 따라 동적으로 결정

**객체 메서드**

```jsx
var obj = {
  a: function () {
    console.log(this);
  },
};
obj.a(); // obj
```

객체 메서드 a 안의 this는 객체를 가리킵니다. 이것은 객체의 메서드를 호출할 때 this를 내부적으로 바꿔주기 때문에 그렇습니다.

단 위의 예제에서 다음과 같이 하면 결과가 달라집니다.

```jsx
var a2 = obj.a;
a2(); // window
```

호출할 때, 호출하는 함수가 객체의 메서드인지 그냥 함수인지가 중요합니다. a2는 obj.a를 꺼내온 것이기 때문에 더 이상 obj의 메서드가 아닙니다.

**call, bind, apply**

```jsx
var obj2 = { c: "d" };
function b() {
  console.log(this);
}
b(); // Window
b.bind(obj2).call(); // obj2
b.call(obj2); // obj2
b.apply(obj2); // obj2
```

명시적으로 this를 바꾸는 함수 메서드 call, bind, apply를 사용하면 this가 객체를 가리킵니다.

**생성자 함수**

```jsx
function Person(name, age) {
  this.name = name;
  this.age = age;
}
Person.prototype.sayHi = function () {
  console.log(this.name, this.age);
};
```

생성자 함수도 함수입니다. 만약 new로 호출하지 않고 그냥 호출한다면 어떻게 될까요?

```jsx
Person("ZeroCho", 25);
console.log(window.name, window.age); // ZeroCho 25
```

일반 함수에서 this가 window(전역 객체)를 가리킵니다. 그래서 this.name과 this.age는 window.name, window.age가 되어버립니다.

이를 막으려면 new Person을 사용해야 합니다.

```jsx
var hero = new Person("Hero", 33); // Person {name: "Hero", age: 33}
hero.sayHi(); // Hero 33
```

이렇게 new를 붙이면 this가 생성자를 통해 생성된 인스턴스(hero 자신)가 됩니다.

**화살표 함수(Arrow Function)**

```jsx
var obj = {
  outer: function () {
    console.log(this); // {outer: ƒ}
    var innerFunc = () => {
      console.log(this); // {outer: ƒ}
    };
    innerFunc();
  },
};
obj.outer();
```

ES6 에서는 함수 내부에서 this가 전역 객체를 바라보는 문제를 보완하고자, this를 바인딩하지 않는 화살표 함수를 새로 도입했습니다. 화살표 함수는 실행 컨텍스트를 생성할 때 this 바인딩 과정 자체가 빠지게 되어, 상위 스코프의 this를 그대로 활용할 수 있습니다.

**이벤트 리스너**

```jsx
document.body.onclick = function () {
  console.log(this); // <body>
};
```

일반 함수인데 this가 window가 아닌 <body>입니다. 이러한 이유는 이벤트가 발생할 때, 내부적으로 this가 바뀐 것 입니다. 내부적으로 바뀐 것이기 때문에 동작을 외울 수 밖에 없습니다.

**제이 쿼리**

```jsx
$("div").on("click", function () {
  console.log(this);
});
```

해당 코드에서 this는 클릭한 div가 됩니다. 내부적으로 함수를 호출할 때 그렇게 this를 바꿔버렸기 때문입니다. 외워야 합니다.

# 예상질문

- 실행 컨텍스트란?
- 함수 호출 방식에 따른 this 바인딩

# Ref

https://www.zerocho.com/category/JavaScript/post/5b0645cc7e3e36001bf676eb

모던 자바스크립트
