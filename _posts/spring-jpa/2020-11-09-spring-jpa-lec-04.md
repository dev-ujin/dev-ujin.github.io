---
layout: post
title: "[Spring+JPA]간단한 쇼핑몰::04.어플리케이션 아키텍처"
date: 2020-11-09 03:17:00 0800
categories: Spring+JPA
tags: Spring JPA 실전스프링부트와JPA의활용1
comments: 1
---
> 

> 김영한님의 [실전스프링부트와JPA의활용1](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1)

## 회원 레포지토리 개발
MemberRepository
- Repository 이름 앞에 `@Repository` annotation을 달아준다

```java
public class MemberRepository {

    @PersistenceContext
    private EntityManager em;

    public void save{}
    public void findOne {}
    public List<Member> findAll() {}
    public LIst<Member> findByName() {}
}
```

## 회원 서비스 개발
- 회원 가입
- 회원 전체 조회
- @Autowired
  - 방법1 바로주입
  - 방법2
```java
    @Autowired
    public void setMemberRepository(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }    
```
- 방법3 : 생성자 주입 (권장)
```java
    private final MemberRepository memberRepository; //final 권장
    @Autowired //최신버전에서는 어노테이션 생략가능
    public MemberServie(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }
```

lombok
  - @AllArgsConstructor
  - @RequiredArgsConstructor : final 잡혀있는 애만 생성자로 만들어줌
- @Transactional : spring에서 제공하는 걸 사용할 것을 권장
- @Transactional(readOnly = true)
  - 데이터 변경할 곳에는 사용하면 안됨
  - 방법 두가지
  - 1. 함수마다 readOnly 적용
  - 2. MemberService 전체를 readOnly로 두고 데이터변경이 필요한 함수에만 @Transactional annotation 따로 붙여줌 (dafault가 readOnly=false임)
  
- 실무에서 고려해야할 점 : validate함수에서 List로 findMember를 부르는데 만약 같은 이름으로 두 개의 쿼리가 동시에 날라왔다면 문제가 발생함 따라서, name을 unique속성으로 주는 것이 안전



# 회원 기능 테스트
- @SpringBootTest는 기본적으로 rollback을 해버리기 때문에 rollback을 원하지 않는다면 @Rollback(false) 값을 줘야함
- rollback이지만 쿼리문을 보고 싶다면
  @Autowired EntityManager em;을 적고 em.flush();를 해주면 insert문을 확인할 수 있음


- 테스트모드로 돌리고 싶을 때 : url: jdbc:h2:mem:test






# 주문
- cascade의 범위를 어디까지 해야해? 의미있는 범위에 대해서 사용해야 함