## 질문 1. **동기와 비동기의 차이는?**

### 동기 Synchronous

요청과 그 결과가 동시에 일어난다. 요청을 보낸 후 응답(=결과)를 받아야지만 다음 동작이 이루어지는 방식이다.

> 순서에 맞춰 진행된다.설계가 매우 간단하다.여러 가지 요청을 동시에 처리할 수 없고 대기해야 한다.
> 

### 비동기 Asynchronous

요청과 결과가 동시에 일어나지 않는다. 요청에 따른 응답을 즉시 처리하지 않아도, 대기 시간동안 다른 요청에 대한 처리가 가능하다.

> 동기 방식보다 속도가 느리고 복잡하다.자원을 효율적으로 사용할 수 있다.
> 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/49ba5954-2cfc-48fc-8ccc-1702dd703bf5/2fe715d2-d520-4cee-bbf6-52a3df3f1afc/Untitled.png)

→ **답변**:  동기는  요청을 보낸 후 응답(=결과)를 받아야지만 다음 동작이 이루어지는 방식입니다.  여러가지 요청을 동시에 처리할 수 없고 순서에 맞춰 진행하기에 설계가 매우 간단하고 직관적이지만 결과가 주어질 때까지 아무것도 못하고 대기해야 하는 단점이 있습니다. 반면 , 비동기는  여러가지 요청을 동시에 처리할 수 있기 때문에 동기 방식보다 속도가 느리고 복잡하지만 자원을 효율적으로 사용할 수 있습니다. 

## 질문 2. **JavaScript의 비동기 과정 은?**

JavaScript의 엔진

- Memory Heap(메모리 힙)
- Call Stack(호출 스택)

### **Call Stack**

프로그램에서 우리가 어디에 있는지, 어떤 일을 해야할 지를 기본적으로 기록하는 일을 수행.

- 작업(함수)을 실행하면 맨 위로 해당 작업(함수)이 추가(`push`)되며, 해당 작업이 끝났으면 **Call Stack**  내에서 ****삭제(`pop`)된다.
- Call Stack에 저장되는 각 항목을 **실행 맥락(Execution Context)**이라 한다.

### **비동기 과정**

1. DOM 이벤트, HTTP 요청, `setTimeOut()` 등과 같은 비동기 함수는 web API를 호출한다.
2. Web API는 콜백 함수를 Event Queue에 넣는다.
3. Task Queue는 대기하다가 Call Stack이 비는 시점에 **Event Loop**를 돌려 Call Stack에 콜백 함수를 넣는다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/49ba5954-2cfc-48fc-8ccc-1702dd703bf5/5555354b-9802-4f27-ba8f-94b79b204a24/Untitled.png)

→ **답변**: Call Stack에 `setTimeOut()` 등과 같은 비동기 함수가 들어오면 브라우저에서 제공하는 멀티쓰레드 방식의 web API를 호출합니다. web API는 비동기 함수들을 수행하고 수행이 끝난 코드들은 대기실과 같은 Event Queue에 콜백함수들을 넣습니다. Call Stack이 비는 시점에 **Event Loop**를 돌려 Call Stack에 콜백 함수를 넣으며 동작합니다. 

## 질문 3. **JavaScript의  비동기 처리는?**

- Ajax : 서버와 통신하기 위해 `XMLHttpRequest` 객체를 사용하는 것.
- **Callback 함수:**  다른 함수의 파라미터로 넘기는 함수 : **콜백 지옥(Callback Hell)** 문제 →`Promise`와 `async/await` 해결
- **Promise:** 비동기 작업의 최종 완료와 그 결과값을 나타내는 객체.  → 여전히 콜백함수 사용
    - 대기(Pending): 이행하지 않거나 거부되지 않은 초기 상태
    - 이행(Fulfilled): 연산이 성공적으로 종료됨
    - 거부(Rejected): 연산이 실패함
- **async/await :**함수 앞에 `async`를 붙이면 해당 함수는 **비동기 함수(async function)**가 되고 반환되는 값은 Promise 객체가 됨. →장점으로 동기식 코드를 짜듯이 비동기 코드를 짤 수 있다.

출처

[https://velog.io/@wngkdroqkf441/Frontend-기술-면접-대비-동기와-비동기](https://velog.io/@wngkdroqkf441/Frontend-%EA%B8%B0%EC%88%A0-%EB%A9%B4%EC%A0%91-%EB%8C%80%EB%B9%84-%EB%8F%99%EA%B8%B0%EC%99%80-%EB%B9%84%EB%8F%99%EA%B8%B0)

[https://inpa.tistory.com/entry/🌐-js-async](https://inpa.tistory.com/entry/%F0%9F%8C%90-js-async)

https://www.youtube.com/watch?v=v67LloZ1ieI&t=53s
