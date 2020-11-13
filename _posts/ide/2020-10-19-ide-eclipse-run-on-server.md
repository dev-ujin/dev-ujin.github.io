---
layout: post
title: "[IDE]Eclipse::Run on Server 활성화"
date: 2020-10-19 12:58:00 0800
categories: IDE
tags: eclipse server
comments: 1
---

> 

# 문제 상황
프로젝트를 실행할 서버를 선택하고 설정해야 하는데 `프로젝트 우클릭 > Run As > Run on Server` 탭이 없음

# 해결 방법
## 1) Dynamic Web Project가 있는 경우 선택
`프로젝트 우클릭 > Properties > Project Facets > Dynamic Web Project` 선택

## 2) Dynamic Web Project가 없는 경우
1. `Help > Install New Software > Work with`에 **http://download.eclipse.org/releases/[eclipse-version]**을 입력
2. **Web, XML, Java EE and OSGi Enterprise Develpment** 선택
3. 필요한 항목에 체크
   - **Eclipse Java EE Developer Tools**
   - **Eclipse Java Web Developer Tools**
   - **Eclipse Web Developer Tools**
   - **Eclipse XSL Developer Tools**