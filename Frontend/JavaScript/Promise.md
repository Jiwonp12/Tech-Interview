# [JavaScript] Promise

- Promise는 JavaScript에서 비동기 처리에 사용되는 객체입니다.
- 비동기 처리란 특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 JavaScript의 특성을 의미합니다.

## Promise가 왜 필요한가요?



Promise는 주로 서버에서 받아온 데이터를 화면에 표시할 때 사용합니다. 일반적으로 웹 어플리케이션을 구현할 때 서버에서 데이터를 요청하고 받아오기 위해 아래와 같은 API를 사용합니다.

```jsx
fetch('url 도메인/진솔/진솔바보', {method: 'GET'});
```

위 API가 실행되면 서버에 데이터를 보내달라는 요청을 보냅니다. 그러나 여기서 데이터를 받아오기도 전에 마치 데이터를 받아온 것처럼 화면에 데이터를 표시하려고 하면 오류가 발생하거나 빈 화면이 나오게 됩니다. 이를 해결하기 위한 방법 중 하나가 Promise입니다.

## Promise의 3가지 상태



Promise를 사용할 때엔 프로미스를 생성하고 종료될 때까지 3가지 상태를 갖습니다.

- Pending(대기): 비동기 처리 로직이 아직 완료되지 않은 상태
- Fulfilled(이행): 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- Rejected(실패): 비동기 처리가 실패하거나 오류가 발생한 상태

### Pending(대기)

```jsx
new Promise();

new Promise(function(resolve, reject) {
 // ...
});
```

`new Promise()` 메서드를 호출하면 대기 상태가 됩니다. `new Promise()` 메서드를 호출할 때 콜백 함수를 선언할 수 있고, 콜백함수의 인자는 `resolve`, `reject`입니다.

### Fulfilled(이행)

```jsx
new Promise(function(resolve, reject) {
	resolve();
});
```

여기서 콜백함수의 인자인 `resolve`를 실행하면 이행 상태가 됩니다.

```jsx
function getData() {
	return new Promise(function(resolve, reject) {
		let data = 100;
		resolve(data);
	});
}

getData().then(function(resolvedData) {
	console.log(resolvedData); // 100
});
```

그리고 이행 상태가 되면 `then()`을 이용하여 처리 결과 값을 받을 수 있습니다.

### Rejected(실패)

```jsx
function getData() {
  return new Promise(function(resolve, reject) {
    reject(new Error("Request is failed"));
  });
}

// reject()의 결과 값 Error를 err에 받음
getData().then().catch(function(err) {
  console.log(err); // Error: Request is failed
});
```

`new Promise()`로 프로미스 객체를 생성하면 콜백함수 인자로 `resolve`와 `reject`를 받을 수 있다고 했습니다. 여기서 `reject`를 호출하면 실패 상태가 됩니다. 그리고, 실패 상태가 되면 실패한 이유(에러)를 `catch()`로 처리를 할 수 있습니다.