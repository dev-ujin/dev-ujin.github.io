---
layout: post
title: "[Javascript]01.Javascript 기초"
date: 2020-11-17 17:27:00 0800
categories: Javascript
tags: Javascript
comments: 1
---
> 


# Javascript
_____
## 특징
- 객체 기반의 스크립트 언어
- HTML로 웹의 내용을 작성, CSS로 웹을 디자인, Javascript로 웹의 동작을 구현
- Node.js와 같은 프레임워크를 사용하면 서버 측 프로그래밍에서도 사용 가능
- 타입을 명시할 필요가 없는 인터프리터 언어





# 기초 문법
_____
### 변수(Variable)
- 대소문자를 구별

### 식별자(Identifier)
- 식별자 : 변수나 함수의 이름을 작성할 때 사용하는 이름
- 숫자로 시작할 수 없음
- 유니코드(Unicode) 문자셋을 사용
- 표현 방법
  1. Camel case
  2. Underscore case
```javascript
// 1. Camel case 방식
var jsVariable = 100;

// 2. Underscore case 방식
var js_variable = 100;
```
### 주석(Comment)
- 표현 방법
  1. 한 줄 주석 : //
  2. 여러 줄 주석 : /* */
- 중첩 주석 : 여러 줄 주석 안에 한 줄 주석은 가능하나, 여러 줄 주석 안에 여러 줄 주석은 불가능