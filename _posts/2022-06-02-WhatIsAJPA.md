---
title: "[jpa] jpa란 무엇인가요?"
excerpt: "jpa란 무엇인가요?"

categories:
  - jpa
tags:
  - [jpa]

permalink: /jpa/WhatIsAJPA/

toc: true
toc_sticky : true

date: 2022-06-02
last_modified_at: 2022-06-02
---

# 'JPA란 무엇인가요?'라는 질문을 하려면 영속성에 대해 알아야 합니다.
<br>

![WhatIsAJPA](/assets/images/posts_img/WhatIsAJPA.png)

---

① 데이터를 사용하려면 데이터는 어딘가에 저장되어야 한다.<br />
② 데이터를 메모리에 저장한다면 시스템이 종료될 때 사라지기 때문에 사용할 수 없다.<br />
③ 데이터를 DB에 저장한다면 시스템이 종료되어도 사용할 수 있다.<br />
④ 데이터가 메모리가 아닌 DB에 저장되어 지속되려는 성질을 **영속성**이라고 한다.<br />
<br />
>**Persistence**
1. [명사] 고집
2. [명사] (없어지지 않고 오래 동안) 지속됨

<br />

## JPA는 데이터를 DB에 저장하기 위한 기술(DB 연동 기술)입니다.

<br>

자바에는 다양한 DB 연동 기술이 있습니다. JDBC, MyBatis, EJB, Hibernate, JPA 등입니다. JPA는 가장 최신 기술입니다.

이 글에서는 JDBC, MyBatis, Hibernate, JPA 순으로 DB 연동 기술을 구현해봅니다. 실습 환경은 아래와 같습니다.
<br>

---

## ⚙️ 실습 환경

Category | stack |
OS | Windows 11 |
IDE | IntelliJ Ultimate [🧷](https://www.jetbrains.com/ko-kr/idea/download/#section=windows) |
Language | Java (openjdk 11.0.6) [🧷] (https://www.azul.com/downloads/?version=java-11-lts&os=windows&architecture=x86-64-bit&package=jdk)|
DB | H2(1.4.199) [🧷](https://h2database.com/html/download-archive.html) |
Build Tool | Maven |
Persistence Framework | JDBC, MyBatis, Hibernate, JPA |



<br>

---

### 참고문헌

**JPA 퀵스타트**

채규태 지음ㅣ루비페이퍼ㅣ2020ㅣ[**도서 정보**](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791186710586&orderClick=LAG&Kc=)
