---
layout: post
title: "[Node/React]Boilerplate 만들기::01.개발환경 구축"
date: 2021-03-01 01:34:00 0800
categories: Node+React
tags: node react boilerplate
comments: 1
changefreq: daily
priority: 1
---

> 

# [1] Node.js와 Express.js
- **Node.js**는 Javascript를 **서버 측면**에서 사용할 수 있도록 해준다.
- **Express.js**는 Node.js를 쉽게 사용할 수 있게 해주는 **프레임워크**이다.

## Node.js 다운로드
- 터미널에 `node -v`를 입력해 컴퓨터에 Node.js가 있는지 확인한다.
- Node.js가 아직 없다면 [Node.js 홈페이지](https://nodejs.org/ko/)에서 다운로드를 받는다.

## 프로젝트 설정
- 프로젝트 디렉토리를 생성 후 `npm init` 명령어를 통해 프로젝트 기본 설정사항을 정해준다.
- 설정 사항에 대해서는 Enter 키를 눌러 default 값으로 두어도 괜찮다.
```shell
mkdir boiler-plate
cd boiler-plate
npm init
```
`package.json`파일이 만들어진 것을 확인할 수 있다. 

## Express.js 다운로드
```shell
npm install express --save
```
`package.json`파일의 `dependencies`에 express가 추가된 것을 확인할 수 있다.

# [2] Hello World 출력해보기
🔽 `index.js` 파일을 만들어 [Express 문서 - Hello world 예제](https://expressjs.com/ko/starter/hello-world.html)의 코드를 복붙한다.

```javascript
// index.js
const express = require('express')
const app = express()
const port = 3000

// root 디렉토리로 들어오면 Hello World!를 출력
app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```
🔽 `package.json` > scripts에 `"start": "node index.js"`(의미: start는 index.js를 노드로 실행하겠다)을 추가한다.

```json
{
  "name": "boiler-plate",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "ujin",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1"
  }
}
```
- 터미널에 `npm run start`로 실행한다.
- 브라우저를 실행해 `localhost:3000`로 들어간다.

# [3] MongoDB 연결
## Cluster 생성
- 회원 가입 후 `Create New Cluster`를 누른다.
- 아래와 같이 설정한다.
  - Cloud Provider: AWS 
  - Region: Free Tier Available 뱃지가 있는 가장 가까운 나라 선택
  - Cluster Tier: M0 Sandbox 선택
  - Cluster Name: 하고 싶은 이름으로
- 5-7분 정도 기다리면 내가 지정한 이름으로 Cluster가 만들어진다.

## Mongoose 다운로드
- MongoDB Cluster가 생성되는 것을 기다리는 동안 `npm install mongoose --save`로 Mongoose를 다운로드 받는다.
- Mongoose는 MongoDB를 편리하게 쓸 수 있도록 해주는 Object Modelling Tool이다.
- `package.json`파일의 `dependencies`에 mongoose가 추가된 것을 확인할 수 있다.

## 프로젝트에 연결하기
- MongDB 사이트의 Cluster에서 `Connect`를 누른다.
- `Add a connection IP address`를 눌러 나의 IP를 접근 가능한 IP 리스트에 넣는다.
- Username과 Password를 지정하고 `Create MongoDB User`를 누른다.(**기억해둬야한다!**)
- `Choose a connection method` > `Connect your application` > `mongdb+srv://`로 시작하는 부분 복사해두기
- `index.js` 파일에 아래 코드를 작성하고 mongoose.connect()에 위에서 복사한 내용을 붙여넣기 하고 \<password>부분을 채운다.

```javascript
const mongoose = require('mongoose')
mongoose.connect('mongodb+srv://<username>:<password>@<clustername>.porkr.mongodb.net/myFirstDatabase?retryWrites=true&w=majority', {
  useNewUrlParser: true, useUnifiedTopology: true, useCreateIndex: true, useFindAndModify: false
}).then(() => console.log('MongoDB Connected...'))
  .catch(err => console.log(err))
```

## 연결 확인하기
- `npm run start`을 눌러 console에 'MongDB Connected...' 메시지가 출력되는지 확인한다.

# [4] 비밀 설정 정보 관리(예: MongoDB 연결 key 분리하기)
- git으로 버전관리를 하면 github에 데이터베이스 연결 정보나, API key 같은 중요한 정보들이 노출되지 않도록 신경써야한다.
- `process.env.NODE_ENV`: 환경설정 변수로 현재 환경이 개발모드인지, 배포모드인지 알려준다.
- 프로젝트에 `config` 폴더를 만들어 각각 `dev.js`, `key.js`, `prod.js` 세 개의 파일을 만든다.

🔽 key.js: process.env.NODE_ENV 변수에 따라 각각 다른 파일에서 export할 수 있도록 경우를 나눈다.
```javascript
if (process.env.NODE_ENV === 'production') {
    module.exports = require('./prod');
}
else {
    module.exports = require('./dev');
}
```
🔽 dev.js: 개발모드인 경우
```javascript
module.exports = {
    mongoURI: 'mongodb+srv://<username>:<password>@<clustername>.porkr.mongodb.net/myFirstDatabase?retryWrites=true&w=majority'
}
```

🔽 prod.js: 배포모드인 경우
```javascript
module.exports = {
    mongoURI: process.env.MONGO_URI
}
```

- `index.js`를 수정한다.

🔽 connect에 필요한 값을 간접적으로 가져올 수 있도록 코드를 바꾼다.
```javascript
const config = require("./config/key") // 추가

mongoose.connect(config.mongoURI, { // 수정
    // 생략
    ...
```
- `.gitignore`에 `dev.js`를 추가한다.


