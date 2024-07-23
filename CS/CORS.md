# CORS (Cross Origin Resource Sharing)

<img src="https://github.com/jinsupark4255/FE-TechInterview/assets/116702892/105265ad-016c-4048-bfa3-e1c24c9e26d6" width="500" height="400">

## CORS의 등장 배경

Origin의 경우 프로토콜 + 도메인 + 포트 번호를 뜻한다.<br>
예전에는 하나의 서버에서 비즈니스 로직과 html 페이지 빌드를 하는것이 일반적이었다.<br>
그 당시에 웹사이트에서 다른 서버로 요청을 날리면, 보안상 악의적인 행동이라고 의심했기 때문에<br>
웹 브라우저는 같은 도메인이 아니면 요청을 막기로 했다.

하지만 날씨 API 같이 점점 다른 도메인으로 브라우저에서 요청을 보내는 일이 많이 생겼고<br>
요청이 막히는 불편함을 없애고자 CORS가 등장하게 되었다.

## CORS란?

웹 페이지가 다른 도메인의 자원에 접근할 수 있도록 허용하는 보안 메커니즘이다.

## CORS 작동 방식

HTTP 헤더를 사용하여 브라우저와 서버가 서로 통신하여, 어떤 출처들이 해당 자원에 접근할 수 있는지 명시하게 된다.<br>
서버는 다음과 같은 CORS 헤더를 포함할 수 있다.

```
- Access-Control-Allow-Origin: 어떤 출처의 웹 페이지가 해당 자원에 접근할 수 있는지 지정. 특정 도메인을 지정하거나 * (모든 도메인)를 사용.
- Access-Control-Allow-Methods: 허용되는 HTTP 메소드(예: GET, POST, DELETE 등)를 지정.
- Access-Control-Allow-Headers: 서버가 승인하는 특정 HTTP 헤더.
```

## 프론트에서 CORS를 어떻게 대처해야 하나?

보통 CORS 문제는 서버의 설정 문제로 인해 발생한다.<br>
하지만 보통 개발할 때 다른 Origin에서 개발을 하게 되고 (React 포트: 3000, 백엔드 포트: 8080)<br>
인증과 같은 민감한 정보를 보낼 때 axios에서 withCredentials:true로 설정해야 한다.<br>
더불어 백엔드도 서버에서 와일드카드(\*)로 Access-Control-Allow-Origin을 사용하지 말아야 한다.<br>
데이터 노출과 CSRF 공격이 일어날 수도 있기 때문이다.
