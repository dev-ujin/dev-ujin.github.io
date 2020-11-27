---
layout: post
title: "[Spring+JPA]온라인 서점 만들기::04.Repository/Service/Test 작성시 주의점"
date: 2020-11-18 08:31:00 0800
categories: Spring+JPA
tags: Spring JPA 실전스프링부트와JPA의활용1
comments: 1
---

> d

- ctrl alt m : extract method
- alt insert : generate contructor
- 비지니스 로직을 엔티티에 두면 데이터베이스를 연결하지 않고 메서드에 집중하여 테스트하는 것이 중요
- 자동 변수 생성 : ctrl alt v

query : 직접 문자를 다뤄야함 짜증
jpa criteria : jpa 표준 스펙, 코드는 줄어들지만 무슨 쿼리문이 만들어지는지 모르겠다

@NotEmpty @Valid BindingResult 
문제 발생시 bindingResult로 넘어감
그 결과를 form에 가져와서 쓸 수 있도록 해줌

아이템 수정은 merge를
- 실무에서는 merge를 잘 안씀

## 변겨 감지와 병합
<html>#C594C5</html>