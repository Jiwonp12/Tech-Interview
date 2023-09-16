# CORS 정책 - 진솔

# 요약

**CORS**(Cross-Origin Resource Sharing)란 동일한 출처가 아닌 곳에서 리소스를 요청할때 발생하는 보안정책입니다. 출처는 웹 페이지의 프로토콜, 호스트, 포트로 정의 되며 이 중 하나만 달라도 동일하지 않은 출처로 판단합니다. 

**SOP**(Same Origin Policy)는 웹 브라우저가 한 출처의 웹 페이지에서 다른 출처의 리소스에 접근하는 것을 제한하는 보안정책으로, 웹 어플리케이션의 보안을 강화하는데 중요한 역할을 합니다.

# 설명

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/49ba5954-2cfc-48fc-8ccc-1702dd703bf5/a85e4e66-3640-4037-b756-207b73006ed6/Untitled.png)

<aside>
✅ https://joke~ 에서 http://localhost:3000 출처로 가져올 수 있는 엑세스가 CORS정책에 의해 차단되었습니다. 요청된 리소스에 'Access-Control-Allow-Origin' 헤더가 없습니다. 불투명한 응답이 필요에 적합한 경우, 요청 모드를 'no-cors'로 설정하여 CORS가 비활성화된 리소스를 가져오십시오.

</aside>

### 여기서 말하는 출처(Origin) 이란?

**Protocol** : http, https

**Host** : 사이트 도메인

**Port** : 포트번호

URL을 구성하는 이 **3가지**가 같으면 동일한 출처입니다.

### SOP(Same-Origin Policy) 동일 출처 정책

동일한 출처에서만 리소스를 공유할 수 있습니다.

즉, 동일 출처 서버에 있는 리소스는 사용가능하지만 다르다면 사용 불가합니다.

### 왜 이런 정책이 필요할까요?

출처가 다른 두 어플리케이션의 소통은 위험합니다. 

만약 출처가 다른 리소스가 공유될 수 있는 상황이라면

해커가 CSRF(Cross-Site Request Forgery), XSS(Cross-Site Scripting) 등의 방법으로

우리가 만든 어플리케이션에서 해커가 심어놓은 코드로 개인정보를 가로챌 수 있습니다.

### 그래서 사실 CORS는 좋은 정책 입니다.

출처가 같은 리소스를 스스로 만들어 사용할 수도 없는 노릇이고

모든 출처를 허용한다면 해커의 공격 위험이 있습니다.

그래서 **CORS**라는 **예외정책**을 만들어서

**SOP**를 위반해도 다른 출처의 리소스를 허용하게 해줄 수 있습니다.

# 예상질문

- CORS가 뭔가요?
- CORS를 겪고 직접 해결해 본 경험이 있으면 말해주세요

# Ref

- CORS 해결법, 동작원리 등 더 자세한 사항을 알고싶다면 아래 블로그 추천합니다.[🌐 악명 높은 CORS 개념 & 해결법 - 정리 끝판왕 👏](https://inpa.tistory.com/entry/WEB-📚-CORS-💯-정리-해결-방법-👏)