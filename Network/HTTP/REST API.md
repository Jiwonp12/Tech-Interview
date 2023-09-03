# 요약

1. REST는 HTTP 프로토콜을 통해 API를 설계하기 위한 아키텍처 스타일이다.
2. REST API는 REST의 원리를 따르는 API이다.

# 설명

## REST란?

REST(Representational State Transfer)의 약자로 자원을 이름으로 구분하여 해당 자원의 상태를 주고 받는 모든 것을 의미한다. HTTP URL(Uniform Resource Identifier)를 통해 자원(URI)을 명시하고, HTTP Method(POST, GET, PUT, DELETE, PATCH 등)를 통해 해당 URI에 대한 CRUD Operation을 적용하는 것을 의미한다.

### REST의 구성 요소

1. 자원(Resource): HTTP URI
2. 자원에 대한 행위(Verb): HTTP Method
3. 자원에 대한 행위의 내용(Representations): HTTP Message Pay Load

### REST의 특징

1. Server-Client(서버-클라이언트 구조)
2. Stateless(무상태)
3. Cacheable(캐시 처리 가능)
4. Layered System(계층화)
5. Uniform Interface(인터페이스 일관성)

### REST의 장단점

**장점**

- HTTP 프로토콜의 인프라를 그대로 사용하여 REST API 사용을 위한 별도의 인프라를 구축할 필요가 없다.
- HTTP 프로토콜의 표준을 최대한 활용하여 여러 추가적인 장점을 가져갈 수 있게 해주고 HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
- Hypermedia API의 기본을 지키면서 범용성을 보장한다.
- REST API 메시지가 의도하는 바를 쉽게 파악할 수 있다.
- 서버와 클라이언트의 역할을 명확하게 분리한다.

**단점**

- 표준이 존재하지 않는다.
- HTTP Method 형태가 제한적이다.

## REST API란?

REST API란 REST의 원리를 따르는 API를 의미한다. REST API를 올바르게 설계하기 위해서는 지켜야 하는 몇가지 규칙이 존재한다. REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있으며 REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그래밍언어로 클라이언트, 서버를 구현할 수 있다.

### REST API의 설계 규칙

1. URI는 동사보다 명사를, 대문자 보다는 소문자를 사용해야 한다.
2. 마지막에 슬래시(/)를 포함하지 않는다.
3. 언더바 대신 하이폰을 사용한다.
4. 파일 확장자는 URI에 포함하지 않는다.
5. id는 하나의 특정 resource를 나타내는 고유값이다.

## RESTFUL이란?

RESTful이란 REST의 원리를 따르는 시스템을 의미한다. REST를 REST답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것이 아니다. 이해하기 쉽고 사용하기 쉬운 REST API를 만들기 위해 사용하며 RESTful 한 API를 구현하는 근본적인 목적이 성ㄴ으 향상에 있는 것이 아니라 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기이니, 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.

### RESTful 하지 못한 경우

- ex1: CRUD 기능을 모두 POST로만 처리하는 API
- ex2: route에 resource, id 외의 정보가 들어가는 경우(/studens/updateName)

# 예상질문

- RESTful API에 대해 설명해주세요.
- REST란? REST API와 RESTful API의 차이점?

# Ref

[https://khj93.tistory.com/entry/네트워크-REST-API란-REST-RESTful이란](https://khj93.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-REST-API%EB%9E%80-REST-RESTful%EC%9D%B4%EB%9E%80)

https://hahahoho5915.tistory.com/54
