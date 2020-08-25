---
layout: post
title:  "Web Server와 WAS"
date:   2020-08-25 21:10:00 0800
categories: Web
tags: Web
comments: 1
---
> Web Server와 WAS의 개념 / 차이점

## Web Server
_____
### 개념
- 하드웨어와 소프트웨어로 구분

1. 하드웨어 : 웹 서버가 설치되어 있는 컴퓨터
2. 소프트웨어 : 웹 브라우저 클라이언트로부터 HTTP 요청을 받아 **정적인 컨텐츠(.html, .jpeg, .css 등)**를 제공

- 예시 : Apache Server, Nginx, IIS(Windows 전용 웹 서버) 등

### 기능
- HTTP 프로토콜을 기반으로 하여 요청을 서비스
- 웹 브라우저 클라이언트에서 요청이 올 때 **가장 먼저** 요청에 대해 처리

1. **정적인 컨텐츠**에 대해 요청이 왔을 때 : 웹 서버가 자원을 제공
2. **동적인 컨텐츠**에 대해 요청이 왔을 때 : 웹 브라우저 클라이언트 요청(Request)을 WAS에게 보내고, WAS가 처리한 결과를 클라이언트에게 전달(Response)


## WAS(Web Application Server)
_____

### 개념
- HTTP 프로토콜을 통해 컴퓨터나 장치에 어플리케이션을 수행해주는 미들웨어(소프트웨어 엔진)
- **동적인 컨텐츠**를 제공
- HTTP 뿐만 아니라 다양한 프로토콜을 처리
- 예시 : Tomcat, JBoss, Jeus, Web Sphere 등

### 용어
- 웹 컨테이너(Web Container) 혹은 서블릿 컨테이너(Servlet Container)라고 불림
- 한국에서는 주로 WAS라고 표현하지만 영어권에서는 Application Server라고 불림

### 기능
- **DB 접속 기능** 제공
- 여러 개의 트랜잭션 관리
- 업무를 처리하는 비지니스 로직을 수행


## Web Server와 WAS를 구분하는 이유
_____
### Web Server만 있다면?
- Web Server는 정적인 컨텐츠만을 처리하기 때문에 동적인 컨텐츠를 처리하려면 클라이언트가 원하는 요청에 대한 결과값을 미리 만들어 놓고 서비스를 해야 함

### WAS만 있다면?
- 정적인 페이지임에도 불구하고 요청이 들어올 때마다 DB에 쿼리를 날려서 결과를 반환해야 함


### Web Server와 WAS의 분리
- Web Server와 WAS를 분리하여 사용
- Web Server를 WAS 앞에 두고 필요한 WAS들을 Web Server에 플러그인 형태로 사용하면 **효율적인 분산 처리** 가능

## REFERENCE
_____
- [https://jeong-pro.tistory.com/84](https://jeong-pro.tistory.com/84)
- [https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html](https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html)
- [https://stackoverflow.com/questions/936197/what-is-the-difference-between-application-server-and-web-server](https://stackoverflow.com/questions/936197/what-is-the-difference-between-application-server-and-web-server)
