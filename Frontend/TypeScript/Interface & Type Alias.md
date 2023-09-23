# Interface & Type Alias - 진솔

# 요약

Type Alias는 모든 타입을 선언할 때 사용할 수 있고
Interface는 객체에 대한 타입을 선언할 때 사용될 수 있다.
차이점은 **확장 가능 여부**이며
확장 불가능한 타입 선언시 Type Alias를
확장 가능한 타입 선언시 Interface를 사용한다.

# 설명

```tsx
//interface
interface Person {
  name: string,
  age?: number
}

// 빈 객체를 Person 타입으로 지정
const person = {} as Person;
person.name = 'Lee';
person.age = 20;
person.address = 'Seoul'; // Error

// type alias
type Person = {
  name: string,
  age?: number
}

// 빈 객체를 Person 타입으로 지정
const person = {} as Person;
person.name = 'Lee';
person.age = 20;
person.address = 'Seoul'; // Error
```

`interface` 와 `type` 은 그 용도가 매우 비슷해 보입니다.

![Screenshot 2023-09-03 at 2.37.15 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49ba5954-2cfc-48fc-8ccc-1702dd703bf5/7ef85c71-c7fa-486b-b0c3-d70a6eed75c6/Screenshot_2023-09-03_at_2.37.15_PM.png)

공식문서에 따르면 두 방법은 매우 유사하나 가장 큰 차이점은

`type` 은 새 프로퍼티를 추가할 수 없고 `interface` 는 항상 확장 될 수 있다는 점입니다.

아래는 예시 코드 입니다.

![Screenshot 2023-09-03 at 2.38.27 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49ba5954-2cfc-48fc-8ccc-1702dd703bf5/7e9c490c-f796-46ed-bbbb-88cf8a5abc2c/Screenshot_2023-09-03_at_2.38.27_PM.png)

`interface`  는 Window라는 같은 식별자를 사용해도 선언 병합이 가능하지만

`type` 은 에러를 발생시킵니다.

![Screenshot 2023-09-03 at 3.01.32 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49ba5954-2cfc-48fc-8ccc-1702dd703bf5/c6bf80cc-e39b-4f5a-bf54-e53f31047d48/Screenshot_2023-09-03_at_3.01.32_PM.png)

공식문서에서는 개인적 취향에 따라 자유롭게 사용가능하지만

`interface` 를 사용하는것을 권장하고 있네요.

![Screenshot 2023-09-03 at 3.13.30 PM.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/49ba5954-2cfc-48fc-8ccc-1702dd703bf5/6208ac39-3efb-4333-b2a8-f243bdedc0f0/Screenshot_2023-09-03_at_3.13.30_PM.png)

타입스크립트 핸드북에 따르면 [확장이 용이해야 한다는 원칙](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle)에 따라 `interface` 사용을 권장하고 있습니다.

```tsx
// 유니온 타입으로 타입 지정
type Union = string | null;

// 함수 유니온 타입으로 타입 지정
type Func = (() => string) | (() => void);

// 인터페이스 유니온 타입으로 타입 지정
type Shape = Square | Rectangle | Circle;

// 튜플로 타입 지정
type Tuple = [string, boolean];
const t: Tuple = ['', '']; // Error
```

하지만 `interface`로 표현할 수 없거나 `유니온`, 또는 `튜플`을 사용해야한다면 `type`을 사용합니다.

# 예상질문

- 타입스크립트를 왜 쓰나요? (본인이 느낀점)
- 타입과 인터페이스의 차이를 아나요?
- 프로젝트 진행 시에 어떤 상황에서 타입을 쓰고 어떤 상황에서 인터페이스를 썼나요?

# Ref

[Documentation - Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)

[타입 별칭 | 타입스크립트 핸드북](https://joshua1988.github.io/ts/guide/type-alias.html#타입-별칭-type-aliases)

[interface vs type alias](https://tecoble.techcourse.co.kr/post/2022-11-07-typeAlias-interface/)

코드예시