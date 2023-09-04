## **Node.js 란 무엇이고** Node.js 동작 방식에 대해 설명해 주세요.

**Javascript를 브라우저 밖에서도 실행할 수 있도록 하는 Javascript의 런타임**입니다. 

### 특성

#### 1.  **비동기 이벤트 주도** Event→action 방식

이벤트 주도 방식이란 이벤트가 발생을 하게 되면 지정한 어떤 작업이 수행되는 방식을 말합니다.  ↔ 운영체제 동작방식 

한 단계씩 진행, 각 단계에 실행할 콜백들을 가진 큐와 비슷.

특정 시간을 할당해서 그시간 만큼 작업을 처리하는 **라운드 로빈 방식**으로 순환

→ 지속적으로 요청을 처리할 수 있도록 동작

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/49ba5954-2cfc-48fc-8ccc-1702dd703bf5/052fd83f-df9d-4ed2-97dd-e6dd5166d156/Untitled.png)

1. timers : 타이머 콜백 담당
2. pending : 이전 루프의 콜백 담당
3. Idle, prepare : 내부의 작업 수행, i/o 폴링 사전 준비
4. Poll:  새로운 i/o 이벤트를 가져와 실행
5. check: setImmediate() 로 스케줄링된 콜백 호출
6. close :  콜백 실행(소켓 종료)

1번  프로그램 종료까지 반복

#### 2. **싱글스레드 논블로킹**

Node.js는 **싱글스레드 논블로킹** 모델로 구성되어 있습니다. 하나의 스레드로 동작하지만, 비동기 I/O 작업을 통해 요청들을 서로 블로킹하지 않습니다. 즉, **동시에 많은 요청들을 비동기로 수행합니다.**

또한 Node.js는 클러스터링을 통해 **프로세스를 포크(fork)하여 멀티스레드인것 처럼 사용될 수 있습니다.** 트래픽에 따라서 프로세스를 포크할 수 있으므로 서버의 **확장성**이 용이하다는 장점을 갖습니다. 

따라서 일부 블로킹 작업들은 `libuv`의 **스레드 풀**에서 수행되기 때문에 완전한 싱글스레드처럼 동작하지 않습니다. 

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/49ba5954-2cfc-48fc-8ccc-1702dd703bf5/f09cec04-e42e-4e82-b67c-868b19c6fc2b/Untitled.png)

*런타임: 특정 언어로 만든 프로그램을 실행할 수 있는 환경.

Node.js의 특성인 이벤트 기반, 논블로킹 I/O 모델들은 모두 **libuv 라이브러리에서 구현되며 그중 논블로킹 I/O 모델**은 Input과 Output이 *관련된 작업등의 블로킹 작업들을 백그라운드에서 수행하고, 이를 비동기 콜백함수로 이벤트 루프에 전달하는 것을 말합니다.

*(http, Database CRUD, third party api, filesystem) 

### 정리

싱글 쓰레드 언어인 자바스크립트의 특성을 고려하고 확장성 있는 네트워크 애플리케이션을 만들 수 있도록 이벤트 주도 방식과 논블로킹 방식을 주도하고 있다. 

### 출처

[https://medium.com/@vdongbin/node-js-동작원리-single-thread-event-driven-non-blocking-i-o-event-loop-ce97e58a8e21](https://medium.com/@vdongbin/node-js-%EB%8F%99%EC%9E%91%EC%9B%90%EB%A6%AC-single-thread-event-driven-non-blocking-i-o-event-loop-ce97e58a8e21)

https://mniyunsu.github.io/node-loop/

https://www.youtube.com/watch?v=1grtWKqTn50

https://www.youtube.com/watch?v=A04zlpL1Uw4
