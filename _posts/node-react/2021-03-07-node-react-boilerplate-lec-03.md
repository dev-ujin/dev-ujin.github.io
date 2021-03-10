---
layout: post
title: "[Node/React]Boilerplate 만들기::02.회원가입/로그인/로그아웃"
date: 2021-03-07 01:11:00 0800
categories: Node+React
tags: node react boilerplate
comments: 1
changefreq: daily
priority: 1
---

> 

# React란?
- Facebook에서 2013년에 배포한 Javascript Library이다.
- Component로 이루어져 있어서 재사용성이 뛰어나다.
- Virtual DOM

# Babel?
최신 자바스크립트 문법을 지원하지 않는 브라우저를 위해 최신 자바스크립트 문법을 구형 브라우저에서 동작할 수 있게 변환 시켜줌.
# Webpack
복잡한 라이브러리와 프레임워크를 번들로 묶어 간단하게 만들어줌
`npx create-react-app`으로 babel과 webpack

# Client와 Server 폴더로 나눔
- client에 들어가서 `npx create-react-app`

# NPM과 NPX
- NPM(Node Package Manager)
  - npm install하면 locally 하거나 globally하게 다운받을 수 있다. 
  - locally는 node_module에 저장됨
  - globally는 컴퓨터에 저장(`npm install -g blabla`)

- 흐름을 보면
  - 원래는 npm isntall -g create-react-app
  - 이제는 npx create-react-app
  - npx이 npm registry에서 create-react-app을 찾아서 다운로드 없이 실행 시켜준다
  - disk space를 낭비하지 않을 수 있고 항상 최신 버전을 사용할 수 있다는 장점이 있다.

# 리액드 폴더 구조
`src` > `App.js` : 첫 화면. 페이지 랜더링
`src` > `index.js` > getElementById("root")
`public` > `index.html` > <div id="root">
- Webpack이 관리하는 부분은 `src`

# Boilerplate를 위한 폴더 구조
## HOC(Higher Order Component)
- 다른 컴포넌트를 갖는 function

강의 자료 참고해서 채우자

# React Router
