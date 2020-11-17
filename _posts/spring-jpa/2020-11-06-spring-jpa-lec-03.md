---
layout: post
title: "[Spring+JPA]간단한 쇼핑몰::03.어플리케이션 아키텍처"
date: 2020-11-06 11:17:00 0800
categories: Spring+JPA
tags: Spring JPA 실전스프링부트와JPA의활용1
comments: 1
---
> 

> 김영한님의 [실전스프링부트와JPA의활용1](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1)

## 계층형 구조
- Controller, Web : 웹 계층
- Sservice : 비지니스 로직, 트랜잭션 처리
- Repository : JPA를 직접 사용하는 계층, 엔티티 메니저 사용
- Domain : 엔티티가 모여 있는 계층, 모든 계층에서 사용

## 패키지 구조
- [프로젝트명]
  - Domain
  - Exception
  - Repository
  - Service
  - Web

## 개발 순서
1. Service, Repository 개발
2. Testcase 작성 및 검증
3. Web 계층에 적용
4. API 개발
5. 성능 최적화


