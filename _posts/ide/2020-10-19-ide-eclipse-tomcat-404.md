---
layout: post
title: "[IDE]Eclipse::Tomcat연동 - HTTP Status 404"
date: 2020-10-19 14:57:00 0800
categories: IDE
tags: eclipse server tomcat
comments: 1
---

> 

# 문제 상황
Tomcat 서버 설정을 하고 실행했는데 HTTP Status 404 에러가 발생!
![http status 404](http://dev-ujin.github.io/assets/res/ide/tomcat-404-05.png)

# 해결 방법
## 우선...
`프로젝트 우클릭 > Run As > Run on Server`로 실행하면 **http://localhost:8080/[프로젝트명]/**로 실행되는데
주소를 **http://localhost:8080/**로 바꿔서 실행
- localhost:8080에서 에러가 발생한다면 1번
- localhost:8080에서는 에러가 발생하지 않는데 localhost:8080/[프로젝트명]에서 에러가 발생한다면 2번

## 1) localhost:8080에서 에러 발생
1. Servers탭에 추가한 `Server명 우클릭 > Properties > General > Switchlocation` 클릭하여 Location을 변경
![location 변경](http://dev-ujin.github.io/assets/res/ide/tomcat-404-01.png)
1. 다시 Servers탭에 추가한 `Server명 더블클릭 > Server Locations > Use Tomcat Installation`을 선택

## 2) localhost:8080/[프로젝트명]에서 에러 발생

> localhost:8080에서 에러가 발생하지 않고 tomcat에 대한 설명과 호랑이 이미지가 나오면 서버가 프로젝트의 파일을 읽어들여 정상적으로 연동이 된 상태이다. 

![tomcat](http://dev-ujin.github.io/assets/res/ide/tomcat-404-04.png)

- 프로젝트명까지 들어왔을 때 에러가 발생한다면 **index파일의 경로를 확인**해볼 것: `프로젝트명 우클릭 > Properties > Deployment Assembly`
- Source에 webapp과 WebContent가 둘 다 기본 Path('/')로 추가되어 있는지 확인
![index파일의 경로](http://dev-ujin.github.io/assets/res/ide/tomcat-404-02.png)

> 프로젝트 폴더에서 webapp폴더나 WebContent폴더에 html파일 혹은 jsp파일을 불러와서 띄우는데 index.jsp파일은 webapp밑에 있는데 내 설정에는 WebContent만 추가되어 있어서 계속 에러가 났던 것이었다.


### 반갑다! Hello World!
![Hello World](http://dev-ujin.github.io/assets/res/ide/tomcat-404-03.png)

