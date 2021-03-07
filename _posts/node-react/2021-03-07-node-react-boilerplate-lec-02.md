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

# 필요한 라이브러리 및 프로그램
## Body Parser
- POST로 요청된 body에서 데이터를 쉽게 추출할 수 있도록 도와준다.
- `npm install body-parser --save`

## Nodemon
- 서버를 재시작하지 않더라도 소스코드의 변경사항을 감지하여 반영해준다.
- `npm install nodemon --save-dev`
- -dev는 개발모드로 사용하겠다는 의미로 nodemon은 `package.json` > `devDependencies`에서 확인할 수 있다.

### Nodemon으로 서버 구동하기
- `package` > `scripts` 에 `"backend": "nodemon index.js"`를 추가한다.
- `npm run backend`로 서버를 실행한다.


## Bcrypt
- 비밀번호 암호화에 사용하는 라이브러리이다.
- `npm install bcrypt --save`

## JSON Web Token
- 토큰을 생성하는데 이용되는 웹 표준이다.
- `npm install jsonwebtoken --save`

## Cookie Parser
- 쿠키에 쉽게 접근할 수 있도록 도와주는 미들웨어이다.
- `npm install cookie-parser --save`

## Postman
- API 테스트에 사용할 수 있는 프로그램으로, 클라이언트에서 받는 값을 대체할 수 있도록 해준다.
- ([Postman 사이트](https://www.postman.com/downloads/))

### Postman 사용법
- Postman 앱을 실행하여 `workspace` 탭으로 들어간다.
- `플러스(+)` 버튼을 눌러 새로운 Request를 생성한다.
- Request Type과 URL을 입력한다.
- `Body` > `raw` 에 로그인 시 클라이언트 측에서 입력될 데이터를 json 형식으로 넣는다.
- `send` 버튼을 눌러 결과를 확인한다.

# 회원가입 기능
```javascript
const bodyParser = require('body-parser')

app.use(bodyParser.urlencoded({extended: true}))
app.use(bodyParser.json())

```
🔽 `index.js`에 register route를 만든다.
```javascript
const {User} = require("./models/User") 

app.post('/api/users/register', (req, res) => {
  const user = new User(req.body)
  user.save((err, doc) => {
    if(err) return res.json({success: false, err})
    return res.status(200).json({
      success:true
    })
  })
})
```

# 비밀번호 암호화 추가
🔽 `User.js`에 추가한다.
```javascript
const bcrypt = require('bcrypt');
const saltRounds = 10;

...

userSchema.pre('save', function(next) { // save가 동작하기 전에
    const user = this;
    if(user.isModified('password')) { // password가 변경될 때만 동작
        bcrypt.genSalt(saltRounds, function(err, salt) {
            if (err) return next(err)
            bcrypt.hash(user.password, salt, function(err, hash) {
                if(err) return next(err)
                user.password = hash // user password를 hash된 값으로 바꿈
                next()
            });
        });
    }
    else next()
})
```

# 로그인 기능
## 로직
1. 클라이언트가 입력한 이메일주소를 데이터베이스에서 찾는다.
2. 데이터베이스에 이메일주소가 있다면 입력한 비밀번호가 맞는 비밀번호인지 비교한다.(❗️주의: 암호화된 비밀번호의 복호화는 불가능하다. 따라서, 입력으로 들어온 비밀번호를 암호화하여 데이터베이스에 저장된 비밀번호와 비교한다.)
3. 비밀번호까지 맞다면 토큰을 생성하여 쿠키에 저장한다.

🔽 `User.js`에 추가한다.
```javascript
const jwt = require('jsonwebtoken');

...

userSchema.methods.comparePassword = function(plainPassword, cb) {
    bcrypt.compare(plainPassword, this.password, function(err, isMatch) {
        if (err) return cb(err)
        cb(null, isMatch)
    })
}

userSchema.methods.generateToken = function(cb) {
    const user = this;
    const token = jwt.sign(user._id.toHexString(), 'secretToken')
    user.token = token
    user.save(function (err, user) {
        if (err) return cb(err)
        cb(null, user)
    })
}
```


🔽 `index.js`에 login route를 만든다.
```javascript
const cookieParser = require('cookie-parser')
app.use(cookieParser());

...

app.post('/api/users/login', (req, res) => {
  User.findOne({ email: req.body.email}, (err, user) => {// 이메일주소로 user 찾기
    if (!user) {
      return res.json({
        loginSuccess: false,
        message: "제공된 이메일에 해당하는 유저가 없습니다."
      })
    }

    user.comparePassword(req.body.password, (err, isMatch) => {// 비밀번호를 비교
      if (!isMatch)
        return res.json({ loginSuccess: false, message: "비밀번호가 틀렸습니다." })
      
      user.generateToken((err, user) => {
        if(err) return res.status(400).send(err);
        
        res.cookie("x_auth", user.token)
        .status(200)
        .json({ loginSuccess:true, userId: user._id })
      })
    })
  })
})
```

# 로그아웃 기능
- `_id`로 해당 User를 찾아서 User의 token을 빈 문자열("")로 만들어 업데이트한다.

🔽 `index.js`에 logout route를 만든다.
```javascript
app.get('/api/users/logout', auth, (req, res) => {
  User.findOneAndUpdate({ _id: req.user._id}, { token: "" }, (err, user) => {
      if (err) return res.json({ success: false, err });
      return res.status(200).send({
        success: true
      })
    })
})
```




