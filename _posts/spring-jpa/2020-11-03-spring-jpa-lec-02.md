---
layout: post
title: "[Spring+JPA]간단한 쇼핑몰::02.도메인 분석 설계"
date: 2020-11-03 15:40:00 0800
categories: Spring+JPA
tags: Spring JPA 실전스프링부트와JPA의활용1
comments: 1
---
> 

> 김영한님의 [실전스프링부트와JPA의활용1](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1)

# 엔티티 설계시 주의점
## 가급적 Setter를 사용하지 말 것
- 변경 포인트가 너무 많아 유지보수가 어려움

## 모든 연관관계는 지연로딩으로 설정할 것
- 즉시로딩(`EAGER`), 지연로딩(`LAZY`)
- 즉시로딩으로 설정하면 SQL을 예측하고 추적하기 어려움
- JPQL을 실행할 때 N+1문제 발생을 야기
- 연관된 엔티티를 함꼐 조회해야하는 경우 `@ManyToOne(fetch = FetchType.LAZY)` 또는 엔티티 그래프 기능을 사용
- OneToOne과 ManyToOne는 default가 EAGER이므로 설정이 필요

## 컬렉션은 필드에서 초기화할 것
- null문제에서 안전
- 하이버네이트는 엔티티를 영속화할 때 컬렉션을 감싸서 하이버네이트가 제공하는 내장 컬렉션으로 변경하는데 임의의 메서드에서 컬렉션을 잘못 생성하거나 수정하면 매커니즘에 문제가 발생할 수 있음

## 테이블, 컬럼명 생성 전략
- 스프링 부트를 사용하면 실제 데이터베이스에 테이블과 컬럼명이 다르게 저장됨
- 대문자를 모두 소문자로, 카멜 케이스를 언더스코어로 바꾸는 방식

### 테이블명, 컬럼명 생성 단계
1. 논리명 생성 : 테이블명, 컬럼명 명시하지 않으면 논리명 적용(`spring.jpa.hibernate.naming.implicit-strategy`)
2. 물리명 적용 : 모든 논리명이 실제 테이블에 적용됨(`spring.jpa.hibernate.naming.physical-strategy`)
- 원하는 형식이 있다면 `spring.jpa.hibernate.naming.physical-strategy`를 class 구현하면 됨


## cascade 옵션
- 연관된 엔티티의 상태 변화를 전파

## 연관관계 메서드