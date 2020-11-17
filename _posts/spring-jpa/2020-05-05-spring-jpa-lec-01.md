---
layout: post
title: "[Spring+JPA]간단한 쇼핑몰::01.프로젝트 환경설정"
date: 2020-11-03 03:17:00 0800
categories: Spring+JPA
tags: Spring JPA 실전스프링부트와JPA의활용1
---
> 

> 김영한님의 [실전스프링부트와JPA의활용1](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81%EB%B6%80%ED%8A%B8-JPA-%ED%99%9C%EC%9A%A9-1)

# 스프링 부트(Spring Boot)
- [스프링 공식 홈페이지](https://spring.io/projects/spring-boot)에서 소개하는 스프링 부트는 다음과 같음
> 스프링 부트는 독립적이고 production-grade하면서, **스프링 기반의 "just run"할 수 있는 애플리케이션을 쉽게 만들 수 있도록 한다.**

- production-grade
  - 주로 기업에서 사용하는 집약적인 시스템
  - 사건을 예측하고 최대한 손실이나 지연 없이 리커버리할 수 있도록 함
  - 반대되는 개념으로는 consumer-grade가 있음

# JPA(Java Persistence API)
- 자바 응용프로그램에서 관계형 데이터베이스의 관리를 표현하는 자바 API로 자바 ORM(Object Relational Mapping)의 표준
- 스프링 부트와 JPA를 조합하면 높은 개발 생산성을 유지하면서 빠르게 자바 웹 어플리케이션을 구현할 수 있음





# 프로젝트 생성
_____
## 프로젝트 설정
- [스프링 부트 스타터](https://start.spring.io/)를 사용하면 프로젝트 환경설정을 쉽게 설정할 수 있음

![스프링 부트 스타터 설정화면](http://dev-ujin.github.io/assets/res/spring-jpa/spring-initializer-setting.png)

- `build.gradle`파일을 보면 프로젝트 설정 요소들을 볼 수 있음

## 프로젝트 불러오기
- intelliJ실행 > import project > 프로젝트의 build.gradle파일 선택

## 프로젝트 실행
- run으로 실행
- port번호를 확인하여 접속 127.0.0.1:8080

```java
2020-03-30 20:41:44.701  INFO 17176 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
```

- IntelliJ 최근 버전에서는 Gradle로 실행하는 것이 기본 설정 -> 실행 속도가 느림 
- 아래와 같이 설정을 변경하면 Java로 바로 실행해서 실행 속도가 빨라짐

![실행 방법 설정 변경](http://dev-ujin.github.io/assets/res/spring-jpa/intellij-run-setting.png)

## lombok 설치와 설정
- intelliJ > Settings > Plugins에서 lombok 설치
- Settings > Compiler > Annotation Processor > enable annotation processing에 반드시 체크






# 프로젝트 살펴보기
_____
## Gradle 의존관계
- 터미널에 입력하여 확인

```html
gradlew dependencies
```
## 라이브러리
- spring-boot-starter-web
  - spring-boot-starter-tomcat : 톰캣(웹서버)
  - spring-webmvc : 스프링 웹 MVC
- spring-boot-starter-thymeleaf : 타임리프 템플릿 엔진
- spring-boot-starter-data-jpa
  - spring-boot-starter-aop
  - spring-boot-starter-jdbc
    - HikariCP 커넥션 풀
  - hibernate + JPA 하이버네이트 + JPA
  - spring-data-jpa : 스프링 데이터 JPA
- spring-boot-starter(공통) : 스프링 부트 + 스프링 코어 + 로깅
- spring-boot
  - spring-core
- spring-boot-starter-logging
  - logback, slf4j
- spring-boot-starter-test : 테스트 라이브러리
  - junit : 테스트 프레임워크
  - mockito : 목 라이브러리
  - assertj : 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
  - spring-test : 스프링 통합 테스트 지원
 




# View 환경 설정
_____
## thymeleaf 템플릿 엔진
- [thymeleaf 공식 사이트](https://www.thymeleaf.org/)
- **정적인 템플릿 파일**은 **resources > static**에 만들고, **동적인 템플릿 파일**은 **resources > templates**에 만듦
- `templates/ + {viewname} + .html`로 만들어 맵핑

## 실습
### HelloController
```java
@Controller
public class HelloController {
    @GetMapping("hello") //"hello"라는 주소로 들어왔을 때
    public String hello(Model model) {//hello 함수를 실행시켜라
        model.addAttribute("data", "hello!!!"); //model객체의 data라는 속성에 "hello!!!"라는 값을 넘겨주고
        return "hello"; //"hello.html"라는 템플릿으로 랜더링하여라
    }
}
```
### hello.html
```html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org"> <!--html의 namespace를 thymeleaf로 지정-->
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
<p th:text="'안녕하세요. ' + ${data}" >안녕하세요. 손님</p> <!--랜더링하면 data를 받아서 보여주고 순수 html로는 '안녕하세요. 손님'을 화면에 띄움-->
</body>
</html>
```

서버를 실행시키고 127.0.0.1:8080/hello로 들어가면 결과를 확인할 수 있음

### index.html
- **resources > static** 밑에 반드시 **"index.html"** 이름으로 만들어야 함 
  (첫 페이지에서 스프링부트가 static > index.html파일을 찾아서 띄워주기 때문)

```html
<!DOCTYPE HTML>
<html>
<head>
    <title>Hello</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
</head>
<body>
<a href="/hello">hello</a>
</body>
</html>
```

### &#127772; Tip
### html 변경사항 서버 재실행 없이 적용시키기
- build.gradle 파일에 dependencies 부분에 다음을 추가하고 서버를 재실행함

```html
implementation 'org.springframework.boot:spring-boot-devtools'
```
- 변경된 html 파일만 리컴파일해주면 됨(Build > Recompile) 





# H2 데이터베이스 설치 및 환경 설정
_____
## H2 데이터베이스
- 가볍고 편리해 개발이나 테스트 용으로 좋음
- 웹 화면 제공
- [h2 데이터베이스 공식 사이트](https://www.h2database.com)에서 다운로드 받아 실행
  - **1.4.199**버전으로 다운받을 것

## 데이터베이스 생성 방법
1. h2 콘솔을 실행
2. 웹에 뜬 URL에서 **port앞 부분을 localhost로 변경** `http://localhost:8082/blabla`
3. **JDBC URL** 부분에 `jdbc:h2:~/jpashop` 이라고 입력하고 **연결**
4. C:\Users\사용자이름 에서 jpashop.mv 파일이 생성된 것을 확인

- 이후에 접속할 때에는 JDBC URL부분에 `jdbc:h2:tcp://localhost/~/jpashop` 입력하여 연결





# JPA와 DB 설정
_____
### application.yml
- 프로젝트의 설정을 명시
- [Spring Boot Reference Documentation](https://docs.spring.io/spring-boot/docs/2.3.0.RELEASE/reference/html/index.html)에서 찾을 수 있음  
- application.properties를 지우고 application.yml파일을 생성하여 다음과 같이 작성

```html
spring:
  datasource:
    url: jdbc:h2:tcp://localhost/~/jpashop
    username: sa
    password:
    driver-class-name: org.h2.Driver

  jpa:
    hibernate:
      ddl-auto: create
    properties:
      hibernate:
#        show_sql: true
        format_sql: true

logging:
  level:
    org.hibernate.SQL: debug
```
- `MVCC=TRUE`는 여러 개가 한번에 접근했을 때 좀 더 빠르게 처리할 수 있게 해줌(권장사항)
- `ddl-auto`을 create으로 설정하면 애플리케이션 실행시점에 가지고 있던 테이블을 지우고 다시 생성
- `show-sql`은 system out으로 나타내고, `org.hibernate.SQL`은 로그에 나타냄. 따라서, org.hibernate.SQL을 쓰는 것이 좋음

## 동작하는지 확인 실습
### Member
```java
@Entity
@Getter @Setter
public class Member {

    @Id @GeneratedValue
    private Long id;
    private String username;
}
```
- @GeneratedValue : DB가 자동생성하도록 해줌

### MemeberRepository
```java
@Repository
public class MemberRepository {

    @PersistenceContext
    private EntityManager em;

    public Long save(Member member) {
        em.persist(member);
        return member.getId();
    }

    public Member find(Long id) {
        return em.find(Member.class, id);
    }
}
```

### MemberRepositoryTest
- MemberRepository를 위한 Test파일(단축키 ctrl + shift + T)

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class MemberRepositoryTest {
    @Autowired MemberRepository memberRepository;

    @Test
    public void testMember() throws Exception {
        //given
        Member member = new Member();
        member.setUsername("memberA");
        memberRepository.save(member);

        //when
        Long saveId = memberRepository.save(member);

        //then
        Member findMember = memberRepository.find(saveId);
    }
}
```

### &#127772; Tip
- Settings > Editor > Live Templates에서 자신만의 템플릿을 만들어 단축키처럼 쓸 수 있음
- Test코드 작성을 쉽게 하기 위해 `tdd`템플릿을 만들고 적용범위 설정

```java
@Test
public void $NAME$() throws Exception {
    //given
    $END$
    //when
    //then
}
```
