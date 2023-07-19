---
title: "[auth] bearerAuth"
excerpt: "bearerAuth"

categories:
  - auth
tags:
  - [auth]

permalink: /auth/bearerAuth/

toc: false

date: 2022-05-02
last_modified_at: 2022-05-02
---

![bearerAuth](/assets/images/posts_img/bearerAuth.png)

토큰(Token)은 사용자를 구별할 수 있는 문자열입니다. 최초 로그인 시 서버가 만들어 줍니다. 서버가 토큰을 만들어 클라이언트에게 반환하면 클라이언트는 이후 요청에 아이디와 비밀번호 대신 토큰을 넘겨 자신의 인증 여부를 증명합니다.<br />
<br />
토큰 기반 인증은 Request Header에 `<TOKEN>`을 명시합니다. Bearer Token은 아래처럼 생겼습니다.<br />

>Authorization: Bearer qpdjfjxhRmsRKwldhkTekdlwprhewpdltmsxhzmsdmfgkftndlTek
 
<br />

---
<br />

## Bearer 인증
<br />
Basic Auth와 비교해서 장단점을 알아볼까요?<br />

### 장점 ① - Basic Auth에 비해 안정성 ↑
<br />
Basic Auth는 ID와 PW를 모든 요청 헤더에 넣어 전달합니다. 물론 Bearer Auth도 모든 요청 헤더에 넣어 전달하는데 보안 측면에서 **조금 더** 안전합니다.<br />


### 장점 ② - 유효기간 관리
<br />
Basic Auth는 유효 기간을 정할 수 없었습니다. Bearer Auth는 유효기간을 관리할 수 있습니다. 이를 통해 `모든 디바이스에서 로그아웃` 기능을 구현할 수 있습니다.<br />


<br>

---

<br>

## 아직 해결되지 못한 단점
<br />

아래 두 개의 단점은 Basic Auth와 동일한 단점입니다.<br />

### 단점 ① - DB 과부화 확률 ↑
<br />

작은 규모의 애플리케이션인 경우 스케일에 대해 고민할 필요는 없지만 서비스가 커지면 DB 과부화 확률이 올라갑니다. 모든 요청이 로그인 요청이기 때문에 요청 수만큼 인증 서버가 작동해야 하기 때문이죠.<br />

### 단점 ② - 인증 서버 단일 장애점
<br />

인증 서버가 단일 장애점(Single Point of Failure)이 될 수 있습니다. 전체 시스템을 가동불가하게 만드는 것이죠.<br />


<br>





---

### 참고문헌

**React.js, 스프링 부트, AWS로 배우는 웹 개발 101**

김다정 지음ㅣ에이콘출판ㅣ2022ㅣ[**도서 정보**](https://product.kyobobook.co.kr/detail/S000061838547)
