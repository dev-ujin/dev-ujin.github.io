---
layout: post
title: "[Spring+JPA]간단한 쇼핑몰::02.도메인 분석 설계"
date: 2020-11-05 15:40:00 0800
categories: Spring+JPA
tags: Spring JPA 실전스프링부트와JPA의활용1
comments: 1
---
> 

> 김영한님의 [실전스프링부트와JPA의활용1](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1)

# 요구사항 분석
_____
[도메인 모델](../assets/res/spring-jpa/domain-model.png)






# 엔티티 클래스 개발
_____
## JPA 기본 Annotation
### 테이블
```java
@Entity // Entity임을 명시
@Getter // lombok 선택
@Setter // lombok 선택
@Table(name = "[DB에 저장될 Table명]")
```

### 기본키
```java
@Id // PK(Primary Key)임을 명시
@GeneratedValue //  PK 자동생성
@Column(name = "[DB에 저장될 Column명]") // id속성에는 관례상 `table명_id`로 많이 사용됨 
```
 
### 내장타입
- 예 : Member와 Address(city, street, zipcode)
```java
@Embeddable // 어딘가 내장될 수 있음 - Address class
@Embedded // 내장된 컬럼임을 명시 - Member의 address column
```

### 참조 관계
- 연관관계의 주인은 FK(Foreign key)가 가까운 쪽으로 선택
- 예 : Member와 Order의 관계에서 연관관계의 주인은 Order
```java
@ManyToOne
@JoinColumn(name = "[조인 컬럼명]")

@OneToMany(mappedBy = "[주인쪽에 있는 자기 클래스의 컬럼명]")
```

### 상속 관계
부모 클래스
```java
@Inheritance(strategy = Inheritancetype.SINGLE_TABLE) //상속 전략
@DiscriminatorColumn(name = "dtype")
```
자식 클래스
```java
@DiscriminatorValue("[자식 클래스을 구분할 값]")
```

### Enum type
- Enum type 컬럼 앞에 명시
```java
@Enumerated(EnumType.STRING) //STRING으로 선택해야 나중에 선택지가 늘어날 시 확장이 가능함

```
## 연관관계 메서드
- 양방향 관계에서 편의를 위해 작성하는 메서드
- 예
```java
// 주문이 생성되면 양방향에 설정해줘야 함
member.getOrders().add(order);
order.setMember(member);

// 한쪽에 누락될 경우에 대비하여 메서드로 표현
// Order Class에
public void setMember(Member member) {
    this.member = member;
    member.getOrders().add(this);
}
```
- 메서드는 컨트롤하는 쪽에 생성하는 것이 좋음 





# 엔티티 설계시 주의점
_____
## 가급적 Setter를 사용하지 말 것
- 변경 포인트가 너무 많아 유지보수가 어려움
- 후에 리펙토링으로 Setter 제거

## 모든 연관관계는 지연로딩으로 설정할 것
- 즉시로딩(`EAGER`), 지연로딩(`LAZY`)
- 즉시로딩으로 설정하면 SQL을 예측하고 추적하기 어려움
- JPQL을 실행할 때 N+1문제 발생을 야기
- 연관된 엔티티를 함께 조회해야하는 경우 `@ManyToOne(fetch = FetchType.LAZY)` 또는 엔티티 그래프 기능을 사용
- OneToOne과 ManyToOne는 default가 EAGER이므로 설정이 필요

## 컬렉션은 필드에서 초기화할 것
- null문제에서 안전
- 하이버네이트는 엔티티를 영속화할 때 컬렉션을 감싸서 하이버네이트가 제공하는 내장 컬렉션으로 변경하는데 임의의 메서드에서 컬렉션을 잘못 생성하거나 수정하면 매커니즘에 문제가 발생할 수 있음

## 테이블, 컬럼명 생성 전략
- 스프링 부트를 사용하면 실제 데이터베이스에 테이블과 컬럼명이 다르게 저장됨
- 대문자를 모두 **소문자**로, 점(.)은 언더스코어(_)로, 카멜 케이스를 **언더스코어**로 바꾸는 방식

### 테이블명, 컬럼명 생성 단계
1. 논리명 생성 : 테이블명, 컬럼명 명시하지 않으면 논리명 적용(`spring.jpa.hibernate.naming.implicit-strategy`)
2. 물리명 적용 : 모든 논리명이 실제 테이블에 적용됨(`spring.jpa.hibernate.naming.physical-strategy`)
- 원하는 형식이 있다면 `spring.jpa.hibernate.naming.physical-strategy`를 class 직접 구현하면 됨


## cascade 옵션
- 연관된 엔티티의 상태 변화를 전파

