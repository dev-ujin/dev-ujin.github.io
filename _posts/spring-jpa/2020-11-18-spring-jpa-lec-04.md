---
layout: post
title: "[Spring+JPA]온라인 서점 만들기::04.Repository/Service/Test 작성시 주의점"
date: 2020-11-18 08:31:00 0800
categories: Spring+JPA
tags: Spring JPA 실전스프링부트와JPA의활용1
comments: 1
---
> 

> 김영한님의 [실전스프링부트와JPA의활용1](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1)


# 구조별 개발 주의점
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

### &#127772; Tip : IntelliJ 단축키
- inline : `Ctrl + Alt + N`

```java
List<Member> result = em.createQuery("select m from Member m", Member.class).getResultList();
return result;

//inline 적용시
return em.createQuery("select m from Member m", Member.class).getResultList();
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


## Test 코드 작성
> Junit4를 사용했음

- Test class 앞에 `@Runwith(SpringRunner.class)` : JUnit과 Spring을 엮어서 테스트
- Test class 앞에 `@SpringBootTest`
- Test class 앞에 `@Transactional` : Rollback으로 실행
- Test class 내부에 `@Autowired`로 MemberService와 MemberRepository를 주입

### 실제 데이터베이스에서 데이터를 확인을 하고 싶을 때
- `@Transactional`는 default로 Rollback(true)에서 실행되기 때문에 데이터 변경 사항이 데이터베이스에 반영되지 않음
- 하지만 확인이 필요하다면, 단위 Test 앞에 `@Rollback(false)` 옵션

### 예상되는 결과가 Exception을 일으킬 때 (2가지 방법)
1. try-catch문을 작성
2. `@Test(expected = IllegalStateException.class)`와 같이 Annotation을 붙임

### 테스트용 데이터베이스를 따로 실행하고 싶을 때
- `test/resources/application.yml`을 따로 만들어 test용 환경을 설정(`url: jdbc:h2:mem:test`)
- test할 때에는 main이 아닌 test에서의 application.yml파일이 우선권을 가짐
- Springboot는 별도의 설정이 없으면 default로 메모리용 데이터베이스를 사용하기 때문에 아래와 같이 설정을 생략해도 같은 결과를 가짐

```html
// test/resources/application.yml
// 나머지 설정은 생략해도 됨
logging:
  level:
    org.hibernate.SQL: debug
    org.hibernate.type: trace
``` 

### &#127772; Tip : IntelliJ 단축키 
- Test code 작성 : `Ctrl + Shift + T`
