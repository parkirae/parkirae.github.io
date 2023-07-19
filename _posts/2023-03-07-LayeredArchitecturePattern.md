---
title: "[Computer Science] LayeredArchitecturePattern"
excerpt: "LayeredArchitecturePattern"

categories:
  - computer science
tags:
  - [computer science]

permalink: /computer-science/LayeredArchitecturePattern/

toc: true
toc_sticky: true

date: 2023-03-07
last_modified_at: 2023-03-07
---

Layered Architecture Pattern은 코드를 어떻게 관리할 것인가에 대한 방법론입니다. 애플리케이션을 구성하는 요소들을 수평으로 나눠 관리합니다. 상위 레이어가 자신의 바로 하위 레이어를 사용하는 식입니다.

예를 들어 볼까요? 요청을 받은 컨트롤러는 서비스를 호출합니다. 서비스는 다시 DB를 호출하죠. DB는 데이터를 반환합니다.

서비스는 DB에서 받은 데이터를 DTO 등으로 가공하여 컨트롤러에게 전달합니다. 컨트롤러는 요청한 클라이언트에게 응답합니다.

이렇게 레이어(층)으로 코드를 분리하여 관리하는 것을 Layered Architecture Pattern이라고 합니다.

![LayeredArchitecturePattern](/assets/images/posts_img/LayeredArchitecturePattern.png)

## 참고문헌

**React.js, 스프링 부트, AWS로 배우는 웹 개발 101**

김다정 지음ㅣ에이콘출판ㅣ2022ㅣ[**도서 정보**](https://product.kyobobook.co.kr/detail/S000061838547)
