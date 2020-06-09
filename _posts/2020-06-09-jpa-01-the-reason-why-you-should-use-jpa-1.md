---
layout: post
title:  "[JPA]01.JPA를 사용해야하는 이유1"
date:   2020-06-09 21:03:00 0800
categories: JPA
tags: JPA 자바ORM표준JPA프로그래밍
---
> 김영한님의 강의를 듣고 공부한 내용을 바탕으로 작성하였습니다.

> 객체지향 언어와 관계형 데이터베이스를 사용하여 개발할 시 발생하는 문제점과 그에 반해 JPA가 갖는 장점을 코드를 통해 이해할 수 있습니다.

#### SQL을 직접 다룰 때 발생하는 문제점
##### 자바를 통한 데이터 접근 방법
- JDBC API
- iBatis(MyBatis)
- 스프링 JDBC Template : SQL Mapper

##### 현재 개발 추세
- 언어는 **객체 지향 언어**를 사용하고, 데이터베이스는 **관계형 DB**를 사용하는 추세
- 따라서, 객체를 관계형 DB에 관리하는 형태
- 객체답게 모델링 할수록 매핑 작업이 늘어나 SQL중심의 생산성이 낮은 개발이 되어버림

##### 문제점
- CRUD SQL 반복 작업
- 객체와 관계형 DB 사이의 차이

##### ORM(Object-Relational Mapping, 객체 관계 매핑)
- 객체는 객체대로, 관계형 DB는 관계형 DB대로 설계하고, ORM 프레임워크가 중간에서 매핑
- 대중적인 언어 대부분에 ORM 기술이 존재

##### JPA(Java Persistent API)
- 자바 플랫폼을 사용하는 응용 프로그래밍에서 관계형 데이터베이스를 표현하는 자바 API ([위키피디아](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%ED%8D%BC%EC%8B%9C%EC%8A%A4%ED%84%B4%EC%8A%A4_API))
- 자바 진영의 ORM 기술 표준
- 전자정부 표준 프레임워크의 ORM 기술도 JPA 사용

###### JPA의 장점
- CRUD SQL을 작성할 필요 없음
- 데이터 저장 계층에서 작성해야 할 코드가 대폭 줄어듬
- SQl이 아닌 객체 중심의 개발이 가능해 생산성과 유지보수가 좋아짐


#### 패러다임의 불일치
- **객체지향 프로그래밍**은 **추상화, 캡슐화, 정보은닉, 상속, 다형성** 등 시스템의 복잡성을 제어할 수 있는 다양한 개념을 제공
- **관계형 데이터베이스**는 데이터 중심으로 구조화, 집합적인 사고가 필요하며, **추상화, 상속, 다형성 같은 개념을 제공하지 않음**

##### 상속
- 객체는 상속 기능을 가지고 있지만 관계형 DB에는 상속이라는 기능이 없음

###### 객체 모델 코드
```java
abstract class Item {
    Long id;
    String name;
    int price;
}

class Album extends Item {
    String artist;
}

class Movie extends Item {
    String director;
    String actor;
}

class Book extends Item {
    String author;
    String isbn;
}
```

###### SQL 코드
```sql
-- Album 객체 저장
INSERT INTO ITEM ...
INSERT INTO ALBUM ...


-- Movie 객체 저장
INSERT INTO ITEM ...
INSERT INTO MOVIE ...
```

###### 처리
1. 부모 객체에서 부모 데이터를 꺼냄
2. ITEM용 INSERT SQL 작성
3. 자식 객체에서 자식 데이터만 꺼내서 ALBUM INSERT SQL 작성
4. (조회)ITEM과 ALBUM 테이블을 조인해서 그 결과로 다시 Album 객체 생성

###### 자바 컬렉션을 이용한다면
```java
list.add(album);
list.add(movie);

Album album = list.get(albumId);
```
- 비교적 간단하게 구현이 가능

##### JPA와 상속
###### JPA 저장
```java
jpa.persist(album);
```
JPA가 SQL를 아래와 같이 두 번 나누어 실행
```sql
INSERT INTO ITEM ...
INSERT INTO ALBUM ...
```

###### JPA 조회
```java
String albumId = "id100";
Album album = jpa.find(Album.class, albumId);
```
JPA가 ITEM과 ALBUM 테이블을 조인
```sql
SELECT I.*, A.*
    FROM ITEM I
    JOIN ALBUM A ON I.ITEM_ID = A.ITEM_ID
```

##### 연관관계
- **객체**는 **참조**를 사용해 다른 객체와 연관 관계를 가짐(**참조에 접근해서 연관된 객체를 조회**)
- **관계형 DB**는 **외래키**를 사용해서 다른 테이블과 연관관계를 가짐(**조인을 사용해서 연관된 테이블을 조회**)

###### 객체를 테이블에 맞춰 모델링
- Member 객체와 연관된 Team 객체를 참조를 통해 조회할 수 없음
- 좋은 객체 모델링을 기대하기 어렵고 결국 객체지향의 특징을 잃어버림

```java
class Member {

    String id;      // MEMBER_ID 컬럼 사용
    Long teamId;    // TEAM_ID FK 컬럼 사용
    String userName;
}

class Team {

    Long id;        // TEAM_ID PK 사용
    String name;
}
```

###### 객체지향 모델링
- 객체 모델은 외래 키가 필요 없고 참조만 있으면 됨
- 테이블은 참조가 필요 없고 외래키만 있으면 됨
- 개발자가 이를 중간에 변환해줘야 함

```java
class Member {
    String id;
    Team team;          // 참조로 연관관계를 맺는다.
    String username;

    Team getTeam() {
        return team;
    }
}

class Team {
    Long id;
    String name;
}
```

##### JPA와 연관관계
```java
//객체 저장
member.setTeam(team);   // 회원과 팀 연관관계 설정
jap.persist(member);    // 회원과 연관관계 함께 저장
```
```java
//조회
Member member = jpa.find(Member.class, memberId);
Team team = member.getTeam();
```

##### 객체 그래프 탐색
- 객체에서 회원이 소속된 팀을 조회할 때 참조를 사용해서 연관된 팀을 찾으면 되는데 이것을 객체 그래프 탐색이라고 함
###### SQL 사용 시
- 처음 실행하는 SQL에 따라 객체 그래프를 탐색할 수 있는 범위가 정해짐
```sql
SELECT M.*, T.*
FROM MEMBER M
JOIN TEAM T ON M.TEAM_ID = T.TEAM_ID 
```
```java
member.getTeam(); //OK
member.getOrder(); //null
```
###### JPA 사용 시
```java
member.getOrder().getOrderItem()... // 자유로운 객체 그래프 탐색
```
##### 엔티티 신뢰 문제
```java
class MemberService {
    ...
    public void process() {

        Member member = memberDAO.find(memberId);
        member.getTeam();                   // 그래프 탐색이 가능
        member.getOrder().getDelivery();    // 값을 도출되더라도 믿고 사용할 수 없음
    }
}
```

##### 비교
- 객체 : 동일성(Identity)비교와 동등성(Equality)비교
- 데이터베이스 : 기본 키의 값으로 각 ROW를 구분

###### 객체의 동일성 비교와 동등성 비교
- 동일성 비교 : **==**, 객체 인스턴스의 주소값 비교
- 동등성 비교 : **equals()**, 객체 내부의 값을 비교

```java
// MemberDAO 코드
class MemberDAO {

    public Member getMember(String memberId) {
        String sql = "SELECT * FROM MEMBER WHERE MEMBER_ID = ?";
        ...
        // JDBC API, SQL실행
        return new Member(...);
    }
}

// 조회한 회원 비교하기
String memberId = "100";
Member member1 = memberDAO.getMember(memberId);
Member member2 = memberDAO.getMember(memberId);

member1 == member2;     //다름
```

###### JPA와 비교
```java
// member1과 member2는 동일성 비교에 성공
String memberId = "100";
Member member1 = jpa.find(Member.class, memberId);
Member member2 = jpa.find(Member.class, memberId);

member1 == member2;     //같음
```