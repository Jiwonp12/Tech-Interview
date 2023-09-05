# 클로저(Closure) - 진솔

# 요약

내부함수가 생명주기를 마감한 외부함수의 지역변수를 참조할 수 있는 내부함수

# 설명

**1.** inner함수가 outer함수 내부에서 정의되고

**2.** inner함수가 outer함수의 변수 outerVar에 접근할 수 있는 상황을 **클로저** 라고 합니다.

```jsx
function outer() {
  const outerVar = 'I am from outer';

  function inner() {
    console.log(outerVar); // 1. inner함수가 outer함수 내부에서 정의되고
  }

  return inner;
}

const innerFunction = outer();
innerFunction(); // 2. 그 inner함수가 outer함수의 변수 outerVar에 접근할 수 있는 상황 => 클로저
```

### 클로저의 원리

자바스크립트에서 함수는 정의될때 자신의 **내부슬롯**에 상위 스코프의 참조를 저장합니다.

따라서, outer함수가 생명주기를 마감하면서 실행컨텍스트에서는 제거되었지만
inner함수는 **내부 슬롯에 상위 스코프의 참조를 저장**하고 있기 때문에
생명주기가 끝난 outer함수의 변수에 접근이 가능합니다.

### 위 예시 코드에 관한 설명

1. outer함수는 innerFunction에게 **inner함수를 반환**하면서 사라지기 때문에
innerFunction은 inner함수 객체를 참조합니다.
2. outer함수는 생명주기를 마감하면서 실행 컨텍스트에서는 제거 되었지만
**렉시컬 환경**(변수 outerVar(상위스코프), inner함수 )은 남아 있게 됩니다.
3. innerFunction는 inner함수 객체를 참조하고 있고 inner함수 객체는 내부슬롯에 outer함수의 렉시컬 환경을 참조하기 때문에 [가비지 컬렉션](https://www.notion.so/d006cdc0d0dd45aeaf68be6347f6e570?pvs=21)의 대상이 되지 않습니다.
4. 따라서 innerFunction에 의해 inner 함수를 호출을 하면 outer 함수의 지역변수인 outerVar를 다시 참조할 수 있게 됩니다.

### **클로저의 조건**

1. 어떤 함수가 상위 스코프의 식별자를 참조하고 있다.
2. 해당 함수의 외부 함수보다 더 오래 살아있다.

### 클로저는 왜 사용할까요?

상태를 의도치 않게 변경되지 않도록 상태를 안전하게 은닉하고
특정 함수에게만 상태 변경을 허용하기 위해 사용합니다.

# 예상질문

- `클로저 🔥`
    - 클로저에 대해서 아나요? 🔥🔥🔥
    - 클로저를 사용하면 뭐가 좋죠? 🔥🔥
    - 클로저를 어떻게 생성하나요? 🔥

# Ref

1. 모자딥다
2. https://poiemaweb.com/js-closure
3. [https://hanamon.kr/javascript-클로저/](https://hanamon.kr/javascript-%ED%81%B4%EB%A1%9C%EC%A0%80/)
4. https://youtu.be/PVYjfrgZhtU?si=ldlkM1wyEjrwgklT
(사실 이 글보다 이 우테코 영상이 999배 좋습니다>.ㅇ)