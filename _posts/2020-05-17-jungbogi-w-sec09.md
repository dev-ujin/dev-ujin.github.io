---
layout: post
title:  "[정보보안기사/필기]09. 사용자 인증"
date:   2020-05-17 22:35:00 0800
categories: 정보보안기사필기
tags: 정보보안 정보보호일반
---
> 알기사 교재의 'section 09. 사용자 인증'을 공부한 내용을 바탕으로 작성하였습니다.

> `키워드` <bl>보충내용</bl> <r>기출에 나온 내용 보충</r>

<style>
bl {
    background-color: #3aa5d3b0;
    border-radius: 3px;
}
r {
    background-color: #d33a4eb0;
    border-radius: 3px;
}
</style>


#### 1. 인증 개념

##### 메시지 인증
- 전달되는 메시지의 이상유무(내용 변경, 순서 변경, 삭제 여부)를 확인할 수 있는 기능
- 메시지 암호화 방식, MAC(Message Authentication Code)방식, 해시 함수를 이용하는 방식 등이 있음

##### 사용자 인증
- 정당한 가입자의 접속인가를 확인하기 위한 인증
- 개인식별과의 차이점

![사용자 인증과 개인 식별](https://dev-ujin.github.io/assets/res/Personal_Identification.png){: .img01}

  - 사용자 인증의 경우에는 B가 다른 제 3자 D에게 A로 가장할 수 있음

###### 사용자 인증의 유형

|유형|설명|예|
|:---:|:---:|:---:|
|Type 1(지식)|주체 본인이 알고 있는 것을 보여줌(Something you know)|패스워드, 핀(PIN)|
|Type 2(소유)|주체 본인이 가지고 있는 것을 보여줌(Sonething you have)|토큰, 스마트카드|
|Type 3(존재)|주체 본인이 나타내는 것을 보여줌(Something you are)|지문|
|(행위)|주체 본인이 하는 것을 보여줌(Something you do)|서명, 움직임|
|Two Factor|위 타입 중에서 두 가지 인증 메커니즘을 결합하여 구현|토큰+PIN|
|Multi Factor|가장 강한 인증으로 세 가지 이상의 인증 메커니즘 사용|토큰+PIN+지문인식|




_____
#### 2. 사용자 인증 기법

##### 1. 지식 기반 인증(What you know)
- 사용자가 알고 있는 어떤 것에 의존하는 인증 기법
- 보안성은 비밀번호의 크기와 랜덤성에 달려 있음
- 장점
  - 다양한 분야에서 사용 가능함 : 지식 기반 기법에 대한 신뢰도와 인식이 높음  
  - 검증 확실성 : 검증 시 애매 모호성이 없음
  - 관리비용의 저렴함 : 사용자의 기억과 시스템에서 보관하고 있는 참조 정보를 이용하므로 별도의 요금이 추가되지 않음
- 단점
  - 소유자가 패스워드를 망각할 수 있음
  - 공격자에 의한 추측이 가능함
  - 사회 공학적 공격에 취약함
 
###### 패스워드(Password)
###### 시도-응답 개인 식별 프로토콜
###### 영지식 개인 식별 프로토콜
###### i-PIN(Internet Personal Identification Number)
##### 2. 소유 기반 인증(What you have)
###### 메모리 카드(토큰)
###### 스마트카드
###### 일회용 패스워드(OTP, One-Time Password)
##### 3. 개체(생물학적) 특성 기반 인증(What you are)
###### 생체인증(Biometrics)




_____
#### 3. 통합 인증 체계(SSO, Single Sign On)
##### 커버로스(Kerberos)
##### 세사미(SESAME)