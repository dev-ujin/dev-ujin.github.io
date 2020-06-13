---
layout: post
title:  "[JPA]01.JPA를 사용해야하는 이유2"
date:   2020-06-09 21:44:00 0800
categories: JPA
tags: JPA 자바ORM표준JPA프로그래밍
---
> 김영한님의 강의를 듣고 공부한 내용을 바탕으로 작성하였습니다.

> JPA가 어떻게 동작하는지, JPA에서 CRUD는 어떻게 하는지, JPA를 사용해야하는 이유에 대해서 학습하였습니다.

<style>
.img01 {width:80%;}
</style>

#### JPA 동작
![JPA 위치](http://dev-ujin.github.io/assets/res/jpa_position.png){: .img01}

#### JPA 표준 명세
- JPA는 인터페이스의 모음
- JPA 2.1 표준 명세를 구현한 3가지 구현체 : 하이버네이트, EClipseLink, DataNucleus

#### JPA를 사용해야하는 이유
##### 생산성
- 자바 컬렉션에 객체를 저장하듯 JPA에게 저장할 객체를 전달
- INSERT SQL를 작성하고 JDBC API 사용하는 지루하고 반복적인 일을 JPA가 대신 처리해줌

###### 저장
```java
jpa.persist(member)
```
###### 조회
```java
Member member = jpa.find(memberId)
```

###### 수정
```java
member.setName("변경할 이름")
```

###### 삭제
```java
jpa.remove(member)
```

##### 유지보수
- JPA가 CRUD 관련 과정을 대신 처리함으로써 개발자가 유지보수해야 하는 코드 수가 줄어듦

##### 패러다임 불일치 해결
- 상속, 연관관계, 객체 그래프 탐색, 비교하기 같은 패러다임 불일치를 해결

##### 성능
- 다양한 성능 최적화 기회 제공
- 어플리케이션과 데이터베이스 사이에 존재함으로 여러 최적화 시도 가능

##### 데이터 접근 추상화와 벤더 독립성
- 데이터베이스 기술에 종속되지 않도록 함
- 데이터베이스를 변경하면 JPA에게 이를 알림으로써 호환이 가능