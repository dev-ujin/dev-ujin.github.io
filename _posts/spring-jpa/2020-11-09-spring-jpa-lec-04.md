---
layout: post
title: "[Spring+JPA]간단한 쇼핑몰::04.회원 관련 기능"
date: 2020-11-18 02:15:00 0800
categories: Spring+JPA
tags: Spring JPA 실전스프링부트와JPA의활용1
comments: 1
---
> 

> 김영한님의 [실전스프링부트와JPA의활용1](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1)

# 기능 구조별 개발 주의점
_____
## Repository 개발
- Repository class 앞에 `@Repository`
- Repository class 내부에 EntityManager 선언
```java
@PersistenceContext
private EntityManager em;

//혹은 EntityManagerFactory 직접 주입도 가능
@PersistenceUnit
private EntityManagerFactory emf;

```

## Service 개발
- Service class 앞에 `@Service`
- Service class 앞에 `@Transactional`
  - 데이터 변경은 반드시 트랜잭션 안에서 실행
  - javax가 아닌 springframework로 import(권장)
  - Service class 앞에는 `@Transactional(readOnly = true)`로 두고 데이터 변경이 필요한 함수 앞에만 `@Transactional`로 두고 사용(권장)
- Service class 내부에 `@Autowired`로 MemberRepository 주입(4가지 방법)
1. 필드 주입
2. 메서드 주입
3. 생성자 주입(권장)
4. Lombok `@RequiredArgsConstructor` : final로 되어 있는 변수만 생성자로 만들어줌
```java
// 1. 필드 주입
@Autowired
public MemberRepository memberRepository;

// 2. 메서드 주입
@Autowired
public void setMemberRepository(MemberRepository memberRepository) {
  this.memberRepository = memberRepository;
} 

// 3. 생성자 주입
private final MemberRepository memberRepository; //final 권장
@Autowired //최신버전에서는 어노테이션 생략가능
public MemberServie(MemberRepository memberRepository) {
  this.memberRepository = memberRepository;
}

// 4. Lombok Annotation
@RequiredArgsConstructor
public class MemberService {
  private final MemberRepository memberRepository;
}

@RequiredArgsConstructor
public class MemberRepository {
  private final EntityManager em;
}
```



## &#127772; IntelliJ 단축키
- inline : Ctrl + Alt + N
```java
List<Member> result = em.createQuery("select m from Member m", Member.class).getResultList();
return result;

//inline 적용시
return em.createQuery("select m from Member m", Member.class).getResultList();
```





# 회원 기능 테스트
- @SpringBootTest는 기본적으로 rollback을 해버리기 때문에 rollback을 원하지 않는다면 @Rollback(false) 값을 줘야함
- rollback이지만 쿼리문을 보고 싶다면
  @Autowired EntityManager em;을 적고 em.flush();를 해주면 insert문을 확인할 수 있음


- 테스트모드로 돌리고 싶을 때 : url: jdbc:h2:mem:test






# 주문
- cascade의 범위를 어디까지 해야해? 의미있는 범위에 대해서 사용해야 함