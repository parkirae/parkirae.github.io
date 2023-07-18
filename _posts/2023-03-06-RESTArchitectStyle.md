---
title: "[Computer Science] RESTArchitectStyle"
excerpt: "RESTArchitectStyle"

categories:
  - Computer_Science
tags:
  - [Computer Science]

permalink: /ComputerScience/RESTArchitectStyle/

toc: true
toc_sticky: true

date: 2023-03-06
last_modified_at: 2023-03-06
---

2000년, Roy Thomas Fielding(이하 필딩) 씨는 컴퓨터과학 박사 졸업을 위해 논문을 씁니다. 제목은 'Architectural Styles and the Design of Network-based Software Architectures'. 우리 말로는 '네트워크 기반 소프트웨어 아키텍처의 스타일과 디자인'입니다.

이 논문은 컴퓨터 과학 디자인 패턴에 혁혁한 공을 세웠습니다. 바로 REST Architecture Style가 이 논문에서 시작됐죠. REST는 Representational State Transfer의 줄임말입니다.

![RESTArchitectStyle](/assets/images/posts_img/RESTArchitectStyle.png)

**RESTful한 API 설계를 위해서는 아래와 같은 제약 조건이 있습니다.**

첫째, Client-Server
둘째, Stateless
셋째, Cache
넷째, Uniform Interface
다섯째, Layered System
여섯번째, Code-On-Demand

**여섯개나 되는 조건을 지켜야하는 이유는 무엇일까요?**

클라이언트가 서비스를 이용하려면 어떤 형식으로 요청을 보내고 응답을 받는지에 대한 정의가 필요합니다. 만약 모든 서비스마다 요청과 응답 방식이 중구난방이라면 요청과 응답 해석하는데 시간이 오래 걸리겠죠.

하지만 제약 조건을 지켜 메서드를 작성하면 클라이언트는 약속된 메서드로 서비스를 이용할 수 있게 됩니다. 불필요한 시간을 줄일 수 있게 됩니다.

<br>

## 참고문헌

[**Academia**](https://www.academia.edu/)
