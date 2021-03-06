---
layout: post
title: "[정보보안기사]필기::06.전자서명과 PKI"
date: 2020-05-17 20:15:00 0800
categories: 정보보안기사
tags: 정보보안 정보보호일반
---
> 알기사 교재 - section 06. 전자서명과 PKI

# [1] 전자서명
____
## 전자서명 형식
1. 공개키 서명방식 : 서명자의 검증정보를 공개하여 누구나 검증할 수 있는 서명방식
   - 서명 생성 및 검증이 간편
2. 중재서명 방식 : 관용 암호방식에 따라 생성과 검증을 제 3자가 중재하는 방식
   - 서명할 때마다 제 3자의 참여가 있어야 하는 불편 

## 전자서명 과정
1) 송신자는 서명 알고리즘을 이용해서 메시지에 서명을 함  
2) 메시지와 서명이 수신자에게 전송됨  
3) 메시지와 서명에 검증 알고리즘을 적용함  
4) 결과가 참이면 받아들여지고 거짓이면 문서는 거절됨 

## 전자서명 서비스

### 메시지 인증
- 안전한 전자서명구조는 메시지 인증을 보장함

### 메시지 무결성
- 메시지가 변경되면 서명이 달라지기 때문에 전체 메시지에 서명을 할 경우에도 보장이 됨
- 현재 전자서명시스템은 해시함수를 이용하여 서명과 검증 알고리즘을 만들기 때문에 무결정이 보장됨

### 부인방지
- 나중에 앨리스가 보낸 사실을 부인하면, 센터는 저장하고 있는 메시지를 제시하여 진위 여부를 확인할 수 있음

### 기밀성
- 전자서명으로 기밀성이 보장되는 통신을 할 수 없음
- 비밀키를 이용하거나 공개키를 이용하여 암호화를 하여 기밀성을 보장할 수 있음

## 전자서명 주요 서비스
1. 위조 불가(Unforgeable) : 합법적인 서명자만이 전자서명을 생성할 수 있어야 함
2. 서명자 인증(User Authentication) : 전자서명의 서명자를 누구든지 검증할 수 있어야 함
3. 부인방지(Non-Repudiation) : 서명자는 서명행위 이후에 서명한 사실을 부인할 수 없어야 함
4. 변경 불가(Unalterable) : 서명한 문서의 내용은 변경할 수 없어야 함
5. 재사용 불가(Not Reusable) : 전자문서의 서명을 다른 전자문서의 서명으로 사용할 수 없어야 함

## 전자서명 구조

### 1. `RSA 전자서명 구조`
- **소인수분해 어려움을 기반**으로 한 전자 서명 방식
- RSA와 달리, 전자서명 구조에서는 개인키와 공개키의 역할이 바뀜(**송신자의 개인키와 공개키를 사용**)

### 2. `ElGamal 전자서명 구조`
- **이산대수 문제**를 이용한 최초의 서명 방식
- 이 서명 방식은 거의 사용되지 않고, DSA(Digital Signature Algorithm)라 알려진 그 변형이 훨씬 많이 사용됨

### 3. `Schnorr 전자서명 구조`
- ElGamal에 기반을 두고 있지만 **서명의 크기를 줄이기 위해** 새로운 구조를 제안한 방식 

### 4. `전자서명 표준(DSS, Digital Signature Standard)`
- **ElGamal 전자서명을 개량한 방식**으로 **이산대수 문제**를 기반으로 함
- **서명과 검증에 소요되는 계산량을 획기적으로 줄인 방식**
- RSA와 달리, 키 교환이나 암호화에는 쓰이지 않으며 **오직 전자서명의 기능만**을 제공하도록 설계된 알고리즘을 사용

### 5. `타원곡선 전자서명 구조(ECDSA, Elliptic Curve Digital Signature Algorithm)`
- **짧은 처리 시간에 짧은 서명 생성이 가능함**

### `KCDSA(Korea Certification-based Digital Signature Algorithm) 전자서명`
- **ElGamal 전자서명을 개선한 방식**으로 **이산대수 문제의 어려움**에 근거한 방식이며 **DSS를 변형한 방식**
- **효율성을 높이고** **스마트카드 이용시에 편리**하도록 하는 것을 중요하게 고려하여 설계됨
- 임의의 길이를 갖는 메시지 정보에 대해 **부가형 전자서명을 생성 및 검증**할 수 있게 해주는 확인서를 이용한 **부가형 전자서명 알고리즘을 규정**하고 있음

## 전자서명 방식

### 1. `메시지 복원형 전자서명`
- 암호화에 서명자의 개인키가 사용되고, 복호화에 서명자의 공개키가 사용됨
- 장점 : 기존의 공개키 암호방식을 이용하므로 별도의 전자서명 프로토콜이 필요하지 않음
- 단점: 각각의 블록에 서명을 해야하므로 많은 시간이 소요되어 실제로는 사용되지 않음

### 2. `부가형 전자서명`
- 메시지의 해시값에 서명자의 개인키를 이용하여 전자서명한 것을 메시지에 덧붙여 전송
- 수신된 메시지를 해시한 결과와 공개키를 이용하여 전자서명을 복호화한 값을 비교하여 검증함
- 장점 : 메시지가 아무리 길더라도 한 번의 서명생성 과정만이 필요하므로 효율적
- 단점 : 전송량이 약간 늘어남 

### 3. `부인방지 전자서명`
- 자체 인증 방식(서명 검증은 검증자가 임의로 할 수 있으며, 누구든지 검증이 가능한 방식)을 배제시켜 서명을 검증할 때 반드시 서명자의 도움이 있어야 검증이 가능

### 4. `의뢰 부인방지 서명`
- 검증을 원하는 임의의 검증자가 부인 과정을 수행할 수 있다는 것에서 기인됨
- 분쟁이 일어났을 때 해결해주는 사람이나 재판관 같은 특정한 자만이 부인 과정을 수행할 수 있도록 만들어야 함

### 5. `수신자 지정 서명`
- 특정 검증자만이 서명을 확인할 수 있되 문제가 있는 경우라도 검증자의 비밀서명 생성정보를 노출시키지 않고 제 3자에게 서명의 출처를 증명함으로써 분쟁 해결 기능을 제공하는 서명 방식
- 서명의 남용을 서명자가 아닌 검증자(수신자)가 통제할 수 있는 서명 방식

### 6. `은닉 서명(블라인드 서명, Blind Digital Signature)`
- 서명문의 내용을 숨기는 서명 방식
- 제공자(provider, 서명을 받는 사람)의 신원과 서명문을 연결시킬 수 없는 익명성을 유지할 수 있음

### 7. `위임 서명(Proxy Digital Signature)`
- 서명자를 대리해서 서명할 수 있는 방식

### 8. `다중서명(Multisignatures)`
- 동일한 전자문서에 여러 사람이 서명하는 것
- 단순 서명을 반복해서 적용하면 서명의 길이가 늘어나고 서명자가 많은 경우 검증 시간이 오래 걸리는 단점을 해결하기 위한 방식

## 전자서명 응용

### 1. 전자투표(Electronic Voting)

### 전자투표 개념
- 선거인 명부로 데이터베이스를 구축한 중앙 시스템에 자신이 정당한 투표자임을 증명하면 컴퓨터망을 통하여 투표를 할 수 있는 방식
- 장점 : 투표율 향상과 투표 결과를 신속히 알 수 있음
- 단점 : 유권자 개인의 인증과 투표 내용의 기밀성 유지
- 현실적으로 실현이 어려움

### 전자투표 구현을 위한 요구사항
1. 완전성 : 모든 투표가 정확하게 집계되어야 함
2. 익명성 : 투표결과로부터 투표자를 구별할 수 없어야 함
3. 건정성 : 부정한 투표자에 의해 선거가 방해되는 일이 없어야 함
4. 이중투표방지 : 정당한 투표자가 두 번 이상 투표할 수 없음
5. 정당성 : 투표에 영향을 미치는 것이 없어야 함
6. 적임성(투표자격제한 선거권) : 투표권한을 가진 자만이 투표할 수 있음
7. 검증 가능 : 선거 결과를 변경할 수 없도록 누구라도 투표 결과를 확인하여 검증해볼 수 있어야 함

### 전자투표 분류

<table>
<thead><tr><td style="width:12%;">구분</td><td style="width:15%;">투표장치</td><td style="width:13%;">선거관리정도</td><td style="width:15%;">기술적쟁점정도</td><td>특징</td></tr></thead>
<tbody>
<tr><td>PSEV 방식</td><td>전자투표기</td><td>상</td><td>하</td><td>이미 정해져있는 기존 투표소에서 투표기를 이용하여 투표를 실시한 후 전자식 투표기록장치를 개표소로 옮겨와 컴퓨터로 결과를 집계</td></tr>
<tr><td>Kiosk 방식</td><td>전자투표기</td><td>중</td><td>중</td><td>정해지지 않은 임의 투표소에서 전자투표, 투표소와 개표소를 온라인으로 연결하여 투표결과는 자동적으로 개표소로 전송되어 자동적으로 집계</td></tr>
<tr><td>REV 방식</td><td>모바일 디지털TV, PC</td><td>하</td><td>상</td><td>가정이나 직장에서 인터넷을 통하여 투표, 투표 결과가 개표소나 중앙관리센터로 보내져 자동적으로 집계</td></tr>
</tbody>
</table>

### 2. 전자입찰 시스템

### 전자입찰 수행 시 문제점
- 네트워크상의 메시지 유출
- 입찰자와 서버 사이의 공모
- 입찰자간의 공모
- 입찰자와 입찰 공무자간의 공모

### 전자입찰 시스템 구현을 위한 요구사항
1. 독립성 : 전자입찰 시스템의 각 구성요소는 자신들의 독자적인 자율성을 보장받아야 함
2. 비밀성 : 네트워크상에서 개별 정보는 각 구성요소 간에 누구에게도 노출되어서는 안됨
3. 무결성 : 입찰 시 입찰자 자신의 정보를 확인 가능하게 함으로써 누락 및 변조 여부를 확인할 수 있어야 함
4. 공평성 : 입찰이 수행될 때 모든 정보는 공개되어야 함
5. 안정성 : 각 입찰 참여자 간의 공모는 방지되어야 하고 입찰 공고자와 서버의 독단이 발생해서는 안됨

## 전자서명으로 해결할 수 없는 문제
- 서명 검증을 할 때 이용하는 공개키가 진짜 송신자의 공개키인지
- `인증서`를 통해 해결할 수 있음
  - 인증서 : 공개키를 메시지로 간주하고, 신뢰 가능한 다른 사람에게 전자서명을 해서 받은 공개키





# [2] PKI(공개키 기반 구조)
______
## PKI 개념
- **공개키 관리를 위한 키 관리 구조**
- **기밀성, 무결성, 접근제어, 인증, 부인방지**를 제공

## PKI 주요 구성요소

### `정책 승인기관(PAA, Policy Approving Authority)`
- 공개키 기반 구조 전반에 사용되는 **정책과 절차**를 생성하여 수립
- 하위 기관들의 정책 준수 상태 및 적정성을 감사

### `정책 인증기관(PCA, Policy Certification Authority)`
- PAA 아래 계층
- **사용자와 인증기관(CA)이 따라야 할 정책을 수립**
- 인증기관의 공개키를 인증하고 인증서, 인증서 폐지 목록 등을 관리

### `인증기관(CA, Certification Authority)`
- PCA 아래 계층
- **사용자의 공개키 인증서를 발행하고 폐지**
- 인증 정책을 수립하고 인증서 및 인증서 효력 정지 및 폐기목록을 관리
- 다른 CA와의 상호 인증을 제공

### `검증기관(VA, Validation Authority)`
- 인증서와 관련된 **거래의 유효성**을 확인
- **검증기관 없이 인증기관만 존재할 수 있으나**, 인증서 기반 응용은 보안측면에서 불완전하다고 간주될 수 있음
- 외주로 운영하거나 인증기관이 직접 운영할 수 있음

### `사용자와 최종 개체(Subjects and End Entities)`
- PKI 내의 사용자는 사람뿐만 아니라 사람이 이용하는 시스템 모두를 의미
- 수행 기능
  - 자신의 비밀키/공개키 쌍을 생성할 수 있어야 함
  - 공개키 인증서를 요청하고 획득할 수 있어야 함
  - 전자 서명을 생성 및 검증할 수 있어야 함
  - 비밀키가 분실 또는 손상되거나 자신의 정보가 변했을 때 인증서 폐지를 요청할 수 있어야 함

### `등록 기관(RA, Registration Authority)`
- 사용자와 CA가 서로 원거리에 위치해 있는 경우, CA 대신 그들의 신분과 소속을 확인하는 기능을 수행
- 사용자의 신분을 확인하고 인증서 요청에 서명을 한 후 인증기관에게 제출하면, 인증기관은 등록기관의 서명을 확인한 후 사용자의 인증서를 발행하여 등록기관에게 되돌리거나 사용자에게 직접 전달함
- **선택적인 요소**로 RA가 없을 때 CA가 그 기능을 수행할 수 있다고 가정함

### `저장소(Repository, Directory)`
- **사용자의 인증서**를 저장하는 일종의 **데이터베이스**
- 사용자의 정보는 저장소에서 포괄적으로 관리되며 디렉터리는 상황에 따라 적절한 접근 제한을 제공함
- 현재 디렉터리 표준형식으로는 `X.500표준 형식`과 이것을 간략화시킨 `LDAP(Lightweight Directory Access Protocol)`

## PKI 형태

### `계층 구조`
- 최상위의 루트 CA가 존재하고 그 아래에 하위의 CA가 계층적으로 존재하는 **트리형태**
- 상위 CA가 하위 CA에 CA인증서를 발행하며, 하위 CA는 상위 CA의 인증정책에 영향을 받음
- **최상위 CA 간의 상호인증은 허용하지만 하위 CA 간의 상호인증은 원칙적으로 배제함**
- 장점 : **국제 간 상호동작을 원활**하게 함

### `네트워크 구조`
- CA 각각이 자신의 인증정책에 따라 독립적으로 존재하는 형태
- CA 간에 인증을 위해 상호인증서를 발행하여 인증서비스를 함
- 단점 : 모든 상호인증이 허용되면 상호인증의 수가 대폭 증가

### `혼합형 구조`
- 각 도메인의 독립적 구성을 허용하면서 서로 효율적인 상호 연동을 보장하는 구조
- 계층 구조와 네트워크 구조의 장점을 취한 방법

## PKI 주요 관리 대상

### 1. `인증서(PKC, Public-Key Cerificate)`
- 전자서명에 사용된 개인키와 상응하는 공개키를 제공하여 그 공개키가 특정인의 것이라는 것을 확신할 수 있는 증거로서의 기능을 수행
- 인증서는 **제 3자(인증기관)가 발행**
- 인증서에는 **개인정보 및 그 사람의 공개키가 기재되고**, **CA의 개인키로 전자서명 되어있음**

### 2. `X.509`
- 인증서 표준 규격
- S/MIME, IP Security, SSL/TLS, SET에 사용됨
- **기본 영역**
  - 버전(Version)
  - 일련번호(Serial Number)
  - 알고리즘 식별자(Algorithm Identifier)
  - 발행자(Issuer)
  - 유효 개시시간(Validity From)
  - 유효 만기시간(Validity To)
  - 주체(Subject)
  - 주체 공개키 정보(Subject Public-Key Information)
  - 알고리즘(Algorithm)
  - 서명(Signature)
- **버전2에 추가된 영역**
  - 인증기관 고유 식별자(Issuer Unique ID)
  - 주체 고유 식별자(Subject Unique ID)
- **버전3에 추가된 영역(확장영역)**
  - 인증기관 키 식별자(Authority Key ID)
  - 주체 키 식별자(Subject Key ID)
  - 키 용도(Key Usage)
  - 개인키 사용 기간(Private Key Usage Period)
  - 확장 키 사용(Extended Key Usage)
  - CRL 배포지점(Certification Revocation List Districution Points)
  - 주체의 대체 이름(Subject Alternative Names)
  - 발행자 대체 이름(Issuer Alternative Names)
  - 기본제한(Basic Constraints)

### 3. `CRL(인증서 폐지 목록, Certificate Revocation List)`
- 저장소 또는 디렉터리에 등재하여 **신뢰 당사자가 언제든지 이 목록을 검색**할 수 있도록 하여야 함
- 인증서 폐지 목록의 버전, 서명 알고리즘 및 발급 기관의 이름, 인증서 발급일, 다음 번 갱신일, 인증서 일련 번호, 폐지 일자, 폐지 사유 등이 포함되어 있음
- 폐기된 인증서는 **인증서 일련번호**에 의해서 확인할 수 있음
- CA가 전자서명을 하여 발행함
- **유효기간 끝나기 전에 인증서를 폐지해야하는 경우**
  1. 사용자의 개인키가 침해당했을 경우
  2. CA가 사용자를 더 이상 인증해줄 수 없는 경우
  3. CA의 개인키가 침해당했을 경우
- **기본 확장자**
  - CA 키 고유 번호
  - 발급자 대체 이름
  - CRL 발급번호
  - 발급 분배점
  - 델타 CRT지시자 : 최근에 취소된 목록만을 저장한 델타 CRL 지시자
- **개체 확장자**
  - 취소 이유 부호
  - 명령 부호 : 해당 인증서를 만났을 경우 취해져야 할 명령
  - 무효화 날짜

### 4. `온라인 인증서 상태 검증 프로토콜(OCSP, Online Certificate Status Protocol)`
- 작업은 **백그라운드에서 자동으로 수행**됨
- **CA에 의해 관리되고 있는 CRL을 검사함**
- **실시간**으로 인증서 상태를 확인할 수 있는 효율적인 방법
- 구성 : **OCSP 클라이언트, OCSP 서버, 인증 서버**
- **순서**  
  1) OCSP 응답 서명 인증서의 **인증서 템플릿 및 발급 속성을 구성**  
  2) 온라인 응답자를 **호스팅 할 컴퓨터에 대한 등록 권한을 구성**  
  3) Window Server 2003 기반 인증기관인 경우에는 **발급된 인증서에서 OCSP 확장을 사용하도록 설정**  
  4) CA의 기관 정보 액세스 확장에 **온라인 응답자 또는 OCSP 응답자의 위치를 추가**  
  5) CA에 대한 **OCSP 응답 서명 인증서 템플릿을 사용하도록 설정**
- `CMP(인증서 관리 프로토콜, Certificate Management Protocol)` : PKI 환경에서 인증서 관리 서비스를 제공하기 위한 PKI의 실체들 간의 통신 프로토콜

