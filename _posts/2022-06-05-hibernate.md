---
title: "[jpa] Hibernate로 DB 연동하기"
excerpt: "Hibernate로 DB 연동하기"

categories:
  - jpa
tags:
  - [jpa]

permalink: /jpa/Hibernate/

toc: true
toc_sticky : true

date: 2022-06-05
last_modified_at: 2022-06-05
---

![Hibernate](/assets/images/posts_img/hibernate.png)

[JPA란 무엇인가요?](https://parkirae.github.io/jpa/WhatIsAJPA/)에서 JPA는 DB 연동 기술'이라고 했습니다. 더 자세히 알아볼까요?<br />


JPA는 Java Persistence API의 줄임말입니다. API는 Application Programming Interface이지요. 하이버네이트는 JPA를 구현한 프레임워크입니다. 하이버네이트 내부적으로는 JDBC API를 사용하죠.<br />

JPA 구현체는 하이버네이트 말고도 EclipseLink, DataNucleus가 있습니다. 하이버네이트를 사용하기 싫다면 언제든 다른 프레임워크로 변경할 수 있습니다.<br />

**하이버네이트는 JPA의 구현체 중 하나다.**<br />

DB연동이 얼마나 편해졌는지 한번 살펴볼까요?<br />


---
<br />
실습 순서는 다음과 같습니다.<br />
<br />
① VO(Value Object) 작성<br />
② Hibernate 메인 설정 파일 작성<br />
③ DAO(Data Access Object) 작성<br />
④ Client 작성<br />

---
<br />
## 1. VO
<br />
VO는 myBatis 실습에서 사용한 것과 동일합니다. 다만 객체와 테이블을 매핑하기 위해 어노테이션이 추가됐습니다.<br />


```java
package com.rubypaper.persistence.hibernate;

import lombok.Data;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.Table;
import java.sql.Timestamp;

@Data
@Table(name = "S_EMP")
@Entity
public class EmployeeVO {

    @Id
    private Long id;

    private String name;

    @Column(name = "START_DATE")
    private Timestamp startDate;

    private String title;

    @Column(name = "DEPT_NAME")
    private String deptName;

    private Double salary;
}

```

<br />

## 2. Hibernate 메인 설정 파일
<br />
myBatis 메인 설정 파일과 비슷합니다.<br />

① 데이터 소스를 설정합니다. 여기서는 H2 DB를 설정했습니다.<br />

② SQL을 설정합니다. Dialect에서 사용하고 싶은 DB를 지정합니다.<br />

③ Entity Class를 등록합니다. 앞서 작성한 EmployeeVO가 Entity Class로 등록됩니다.<br />


```xml
<?xml version='1.0' encoding='utf-8'?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN" "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">

<hibernate-configuration>

    <session-factory>
        <!--  DataSource 설정 -->
        <property name="hibernate.connection.driver_class">
            org.h2.Driver</property>
        <property name="hibernate.connection.url">
            jdbc:h2:tcp://localhost/~/test</property>
        <property name="hibernate.connection.username">sa</property>
        <property name="hibernate.connection.password"></property>
        <property name="hibernate.connection.pool_size">1</property>

        <!-- Hibernate 프로퍼티 설정 -->
        <property name="hibernate.dialect">
            org.hibernate.dialect.H2Dialect</property>
        <property name="hibernate.hbm2ddl.auto">update</property>
        <property name="hibernate.show_sql">true</property>

        <!-- Entity Class 등록 -->
        <mapping class="com.rubypaper.persistence.hibernate.EmployeeVO" />
    </session-factory>

</hibernate-configuration>
```
<br />

## 3. DAO
<br />
myBatis DAO와 비슷합니다.<br />

Hibernate를 사용하려면 Session 객체가 필요합니다. Session 객체는 아래 방법으로 얻을 수 있습니다.<br />
<br />
① hibernate-cfg.xml을 로딩하여 SessionFactory를 생성합니다.<br />

② SessionFactory의 openSession()을 통해 Session을 생성합니다.<br />


```java
package com.rubypaper.persistence.hibernate;

import java.util.List;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

public class EmployeeDAO {
    private SessionFactory sessionFactory;
    private Session session;
    private Transaction transaction;

    public EmployeeDAO() {
        String config = "com/rubypaper/persistence/hibernate/hibernate.cfg.xml";
        sessionFactory = new Configuration().configure(config).buildSessionFactory();
        session = sessionFactory.openSession();
        transaction = session.getTransaction();
    }

    public void insertEmployee(EmployeeVO vo) {
        System.out.println("===> Hibernate 기반으로 직원 등록");
        try {
            transaction.begin();
            session.persist(vo);
            transaction.commit();
        } catch (Exception e) {
            transaction.rollback();
        }
    }

    public List<EmployeeVO> getEmployeeList() {
        System.out.println("===> Hibernate 기반으로 직원 목록 조회");
        String jpql = "select e from EmployeeVO e order by e.id";
        List<EmployeeVO> employeeList = session.createQuery(jpql).getResultList();
        return employeeList;
    }
}
```

<br />

## 4. Client
<br />
myBatis Client와 비슷합니다. 다만 `vo.setId(4L);`로 식별자값을 넣는 코드가 추가되었습니다.<br />


```java
package com.rubypaper.persistence.hibernate;

import java.sql.Timestamp;
import java.util.List;

public class EmployeeServiceClient {

    public static void main(String[] args) {
        EmployeeVO vo = new EmployeeVO();
        vo.setId(4L);
        vo.setName("고길동");
        vo.setStartDate(new Timestamp(System.currentTimeMillis()));
        vo.setTitle("과장");
        vo.setDeptName("총무부");
        vo.setSalary(2500.00);

        EmployeeDAO employeeDAO = new EmployeeDAO();
        employeeDAO.insertEmployee(vo);

        List<EmployeeVO> employeeList = employeeDAO.getEmployeeList();
        for (EmployeeVO employee : employeeList) {
            System.out.println("---> " + employee.toString());
        }
    }
}
```

<br />

### Hibernate 장점
<br />
### 장점
<br />
**테이블 구조 변경**이 용이합니다.<br />
새로운 정보를 추가하고 싶다면 EmployeeVO Class에 변수를 추가하면 됩니다. 이게 다입니다. DAO나 SQL을 수정할 필요가 없습니다.<br />
<br />

다음 글에서는 ORM 표준인 JPA로 DB 연동을 해보겠습니다.


---

### 참고문헌

**JPA 퀵스타트**

채규태 지음ㅣ루비페이퍼ㅣ2020ㅣ[**도서 정보**](http://www.kyobobook.co.kr/product/detailViewKor.laf?ejkGb=KOR&mallGb=KOR&barcode=9791186710586&orderClick=LAG&Kc=)
