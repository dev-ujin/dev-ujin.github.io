---
layout: post
title:  "00.SpringBoot란, JPA란, 프로젝트 시작하기"
date:   2020-05-05 03:17:00 0800
categories: SpringBoot
tags: SpringBoot JPA 실전스프링부트와JPA의활용1
---
> 김영한님의 강의를 듣고 공부한 내용을 바탕으로 작성하였습니다.

#### 스프링 부트(Spring Boot)
- [스프링 공식 홈페이지](https://spring.io/projects/spring-boot)에서 소개하는 스프링 부트는 다음과 같음
> 스프링 부트는 독립적이고 production-grade하면서, 스프링 기반의 "just run"할 수 있는 애플리케이션을 쉽게 만들 수 있도록 한다.

- production-grade
  - 주로 기업에서 사용하는 집약적인 시스템
  - 사건을 예측하고 최대한 손실이나 지연 없이 리커버리할 수 있도록 함
  - 반대되는 개념으로는 consumer-grade가 있음

#### JPA(Java Persistence API)
- 자바 응용프로그램에서 관계형 데이터베이스의 관리를 표현하는 자바 API로 자바 ORM(Object Relational Mapping)의 표준
<br/>
- 스프링 부트와 JPA를 조합하면 높은 개발 생산성을 유지하면서 빠르게 자바 웹 어플리케이션을 구현할 수 있음

#### 프로젝트 시작하기
##### 프로젝트 설정
- [스프링 부트 스타터](https://start.spring.io/)를 사용하면 프로젝트 환경설정을 쉽게 설정할 수 있음
- Project : Gradle Project
- Language : Java
- Spring Boot : 2.1.13
- Project Metadata
  - Group : jpabook
  - Artifact : jpashop
  - Name : jpashop
  - Description : Demo project for Spring Boot
  - Package name : jpabook.jpashop
  - Packaging : jar
  - Java : 8
- Dependencies에는 아래 5가지를 추가
  - Spring Web
  - Thymeleaf
  - Spring Data JPA
  - H2 Database
  - Lombok
- GENERATE를 눌러 다운로드 받음
- build.gradle파일을 보면 프로젝트 설정 요소들을 볼 수 있음

##### 프로젝트 불러오기
- intelliJ실행 > import project > 프로젝트의 build.gradle파일 선택

##### 프로젝트 실행
- run으로 실행
- port번호를 확인하여 접속 127.0.0.1:8080

```java
2020-03-30 20:41:44.701  INFO 17176 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
```

##### lombok 설치와 설정
- intelliJ > Settings > Plugins에서 lombok 설치
- Settings > Compiler > Annotation Processor > enable annotation processing에 반드시 체크
