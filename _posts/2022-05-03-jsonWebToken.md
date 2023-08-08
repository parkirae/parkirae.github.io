---
title: "[auth] jsonWebToken"
excerpt: "jsonWebToken"

categories:
  - auth
tags:
  - [auth]

permalink: /auth/jsonWebToken/

toc: true

date: 2022-05-03
last_modified_at: 2022-05-03
---

![jsonWebToken](/assets/images/posts_img/jsonWebToken.png)


Basic Auth, Bearer Auth의 공통된 단점은 **'스케일 문제를 해결할 수 어렵다'**는 것입니다. JSON Web Token(이하 JWT)은 스케일 문제를 해결합니다.<br />

JWT는 전자 서명(Digital Signature)된 토큰입니다. JSON 형태로 이뤄져 있습니다. JWT는 `{header}`, `{payload}`, `{signature}`로 구성돼 있습니다.<br />

아래 토큰을 보면 Bearer 토큰과 별 차이가 없어보입니다. 심지어 앞에 `Bearer`라고 명시돼 있기도 합니다. 다른 점은 볼드처리된 문자열 `asdfgqwerty.`입니다. 이걸 전자 서명이라고 합니다.<br />

<br />

>Authorization: Bearer **asdfgqwerty.** qpdjfjxhRmsRKwldhkTekdlwprhewpdltmsxhzmsdmfgkftndlTek.**qqqqqqqqqqqqqqqq.**

<br />


## 전자서명
<br />
서명하고 싶은 메시지를 해시함수를 이용해 축약한 후 개인키로 암호화했을 때 나오는 값을 말합니다.<br />

## JWT 디코딩
<br />

인코딩된 JWT를 Base64로 디코딩하고 각각의 값의 의미를 알아보겠습니다.<br />

>Authorization: Bearer **asdfgqwerty.** qpdjfjxhRmsRKwldhkTekdlwprhewpdltmsxhzmsdmfgkftndlTek.**qqqqqqqqqqqqqqqq.**
 
<br />

```js
{ // header
  "typ": "JWT",
  "alg": "HS512"
},
{ // payload
  "sub": "546546574869465465",
  "iss": "demo app",
  "iat": "54564654",
  "exp": "54564654"
}.
qqqqqqqqqqqqqqqq
// signature
```

<br>

### Header
<br />

- typ: Type. 토큰의 타입을 의미합니다.<br />
- alg: Algorithm. 토큰의 서명을 발행하기 위해 사용된 해시 알고리듬 종류를 의미합니다.<br />

### Payload
<br />
- sub: Subject. 토큰의 주인을 의미합니다. 유일한 식별자여야 합니다.<br />
- iss: Issuer. 토큰을 발행한 주체를 의미합니다.<br />
- iat: issued at. 토큰이 발행된 날짜와 시간을 의미합니다.<br />
- exp: expiration. 토큰이 만료되는 시간을 의미합니다.<br />

### signature
<br />

토큰을 발행한 주체(Issuer)가 발행한 서명입니다. 유효성 검사에 사용합니다.<br />

<br />

---

<br>

## JWT 사용하는 이유
<br />

JWT를 사용하는 이유는 Basic Auth, Bearer Auth의 단점을 극복했기 때문입니다. Basic Auth, Bearer Auth의 공통된 단점은 스케일 문제를 해결할 수 없다는 것입니다. 모든 요청 헤더에 인증 정보를 넣어 전달하고 매번 인증을 받아야 하죠. 인증 서버 과부하 확률이 올라갑니다. JWT는 이 문제를 어떻게 해결했을까요?<br />

<br />

## JWT 인증 방식
<br />

JWT도 Bearer Auth와 마찬가지로 토큰 기반 인증입니다. 토큰 기반 인증에서 토큰은 서버가 생성합니다. JWT도 서버가 토큰을 생성합니다. Bearer Auth와 다른 점은 **JWT는 헤더와 페이로드를 생성한 후, 전자 서명을 한다는 점**입니다.<br />


① 클라이언트가 로그인을 요청합니다.<br />

② 서버는 유저 정보 바탕으로 `{header}`, `{payload}` 작성합니다.<br />
(이때 사용된 유저 정보는 인증된 클라이언트의 유저 정보입니다. 다시 말해, 원래 회원이었던 사람의 정보입니다.)<br />

③ 서버는 ②에서 작성한 값을 `secret key`로 `전자 서명`을 합니다.(이 값을 X라고 하겠습니다.)<br />

④ 서버는 `{header}`, `{payload}`.X를 Base64로 인코딩하고 클라이언트에 반환합니다.<br />

⑤ 클라이언트가 또다른 요청을 합니다. 이때 클라이언트는 ④에서 받은 `<TOKEN>`을 가지고 요청 헤더에 함께 보냅니다.<br />

⑥ 서버는 요청 헤더에 있는 `<TOKEN>`을 Base64로 디코딩합니다.<br />

⑦ 서버는 디코딩해서 얻은 JSON을 `{header}`, `{payload}`, `{signature}`로 나눕니다.<br />

⑧ 서버는 `{header}`, `{payload}`와 자신이 가진 `secret key`로 전자 서명을 생성합니다.<br />

**⑨ 서버가 방금 만든 전자 서명과 HTTP 요청이 가지고 온 `{signature}`를 비교해, 유효성을 검사합니다.**<br />

**⑩ `{signature}`가 일치한다면 토큰이 위조되지 않았다는 뜻이므로 더이상 유효성 검사를 진행하지 않습니다.**<br />


>⑨, ⑩의 과정이 JWT가 스케일 문제를 극복한 이유입니다.<br />
물론 MITM에는 여전히 취약합니다. 그래서 JWT도 반드시 HTTPS를 통해 통신해야 합니다.

<br />



---

### 참고문헌

**React.js, 스프링 부트, AWS로 배우는 웹 개발 101**

김다정 지음ㅣ에이콘출판ㅣ2022ㅣ[**도서 정보**](https://product.kyobobook.co.kr/detail/S000061838547)
