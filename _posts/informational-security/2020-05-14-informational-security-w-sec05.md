---
layout: post
title: "[정보보안기사]필기::05.해시함수와 응용"
date: 2020-05-17 17:47:00 0800
categories: 정보보안기사
tags: 정보보안 정보보호일반
---
> 알기사 교재 - section 05. 해시함수와 응용

# [1] 일방향 해시함수
_____
## 일방향 해시함수의 개념
해시함수는 **임의의 길이의 메시지를 고정된 길이의 해시값 또는 해시코드로 출력**하는 함수<br>
해시함수 h : D &#8594; R (|D| > |R|)는 다대일 대응함수로 **충돌이 반드시 존재**함

## 일방향 해시함수의 특징
1. **임의의 길이의 메시지로부터 고정 길이의 해시값을 계산**
2. 해시값을 **고속으로 계산**
3. `일방향성`(해시값으로부터 메시지를 역산할 수 없는 성질)을 가짐
4. **메시지가 다르면 해시값도 다름**
   - **무결성 확인**을 위해 사용함
   - `충돌(Collision)` : 2개의 다른 메시지가 같은 해시값을 가짐
   - `충돌 내성(Collision Resistance)` : 충돌 발견이 어려운 성질

## 일방향 해시함수의 보안 요구사항
### `프리이미지 저항성(역상 저항성)`
- 임의의 해시값 y에 대해 y = h(M)을 만족하는 입력값 M을 찾는 것이 계산적으로 불가능

### `제 2프리이미지 저항성(두번째 저항 저항성, 약한 충돌 내성)`
- 주어진 입력값 M에 대해 h(M) = h(M'), M &#8800; M'를 만족하는 M'를 찾는 것이 계산적으로 불가능
- 발생 확률이 충돌 저항성보다 낮기 때문에 약한 충돌 내성이라고 부름

### `충돌 저항성(충돌 회피성, 강한 충돌 내성)`
- h(M) = h(M')를 만족하는 두 입력값 M, M'를 찾는 것이 계산적으로 불가능

### 전자서명에 이용되는 특성
- 해시값을 고속으로 계산할 수 있음
- `약 일방향성(Weak Onewayness)` : 프리이미지 저항성
- `강 일방향성(Strong Onewayness)` : 제 2프리이미지 저항성
- `충돌 회피성` : 충돌 저항성
- 약 일방향성과 강 일방향성은 해시 함수의 역함수를 계산하는 것을 방지하는 기능이고, 충돌 회피성은 내부부정을 방지하기 위한 것임

## 일방향 해시함수의 분류

1. `키가 없는 해시함수`

### 전용 해시함수
- **처음부터 새로 만드는 것**
- MD4를 기초로 SHA-1, RIPEMD, RIPEMD-128, RIPEMD-160, HAVAL을 디자인
1. `메시지 다이제스트(Message Digest)`
   - 공개키 기반 구조를 만들기 위해 Rivest교수가 RSA와 함께 개발함
   - MD5는 **메시지를 512비트의 블록들로 나누고**, **128비트 다이제스트를 출력함**
   - MD5는 **내부 구조에서의 약점과 생일공격에 노출**

2. `SHA(Secure Hash Algorithm)`
   - **DSS(Digital Signature Standard)에 사용하기 위해** NSA가 설게하고 NIST에 의해 배포됨
   - **가장 널리 사용됨**
   - **SHA-1의 강한 충돌 내성이 깨져서 대체하는 SHA-3을 제정하기로 함**
   - SHA 알고리즘 비교

    |구분|SHA-1|SHA-224|SHA-256|SHA-384|SHA-512|
    |:---:|:---:|:---:|:---:|:---:|:---:|
    |MD의 길이|160|224|256|384|512|
    |최대 메시지 길이|2<sup>64</sup>-1|2<sup>64</sup>-1|2<sup>64</sup>-1|2<sup>128</sup>-1|2<sup>64</sup>-1|
    |블록 길이|512|512|512|1024|1024|
    |워드 길이|32|32|32|64|64|
    |단계 수|80|64|64|80|80|
    
    - SHA-1은 MD5의 구조를 따르고, 유사한 처리과정을 수행
    - SHA-2는 SHA-1과 하부구조가 동일하며, 동일한 유형의 모듈러 연산과 논리적 2진 연산을 사용

3. `RIPEMD-160 (Race Integrity Primitives Evaluation MD)`
   - **160비트 MD를 생성**
   - **RIPEMD의 강한 충돌 내성은 깨졌지만, RIPEMD-160은 깨지지 않았음**

4. `Tiger`
   - **64비트 시스템에서 해시 함수를 수행하기 위해 설계됨**
   - **MD5, SHA-1보다 더 속도가 빠름**

5. `HAVAL`
   - **1024비트의 블록들로 128, 160, 192, 224, 256비트의 MD출력**

- 주요 해시 알고리즘 비교

|구분|MD5|SHA-1|RIPEMD-160|
|:---:|:---:|:---:|:---:|
|MD의 길이|128비트|160비트|160비트|
|처리 단위|512비트|512비트|512비트|
|단계수|64(16번의 4라운드)|80(20번의 4라운드)|160(16번의 5병행 라운드)|
|최대 메시지 크기|무한|2<sup>64</sup>-1비트|2<sup>64</sup>-1비트|
|앤디언|Little-Endian|Big-Endian|Little-Endian|

- `Big-Endian` : 최상위비트(MSB)부터 부호화되어 저장
- `Little-Endian` : 최하위비트(LSB)부터 부호화되어 저장

### 블록함수 기반 해시함수
- **해시함수 내 압축함수 자리에 대칭키 블록암호를 사용하는 해시함수**
- 새로운 압축함수를 만들 필요 없이 DES, AES같은 알고리즘을 사용할 수 있음

### 모듈연산 기반 해시함수
- **해시함수 내 압축함수 자리에 모듈 연산을 반복하여 사용하는 해시함수**
- 장점 : 하드웨어나 소프트웨어 **자체에 내장된 모듈 연산을 사용**할 수 있음
- 단점 : **속도가 빠르지 않고** **안전성 연구에 대한 역사가 짧음**

2. `키가 있는 해시함수`
- **메시지 인증 기능**을 가진 함수
- **함수 자체에 안전성과 키의 비밀성**에 그 안전성을 두고 있음
- 블록 암호에 기반을 둔 메시지 인증 알고리즘 중 **가장 널리 사용되는 방법은 CBC임**

## 일방향 해시함수의 응용
- 무결성 점검
  - 암호학적 해시함수를 사용해 생성된 새로운 MD와 이전의 MD를 비교하여 그 두 개가 동일하다면 원래 메시지가 변경되지 않은 것임
- 소프트웨어 변경 검출
  - 소프트웨어를 입수한 후, 손으로 해시값을 계산해서 그 값을 오리지널 사이트에서 제공하는 해시값과 비교
- 메시지 인증 코드
  - 메시지 인증은 일반적으로 키가 있는 해시함수로 알려진 메시지 인증코드(Message Authentication Code)를 사용하여 얻어짐
  - 상호 간에 교환되는 정보를 인증하기 위해 비밀키를 공유하는 두 통신 상대자 간에 사용됨
  - SSL/TLS에서도 이용됨
- 전자서명 : 현실 사회의 서명이나 날인에 해당하는 행위를 디지털세계로 가져온 것

## 랜덤 오라클 모델(Random Oracle Model)
- 해시함수에 대한 이상적인 수학적 모델

### 랜덤 오라클 모델의 성질
- 임의의 길이의 메시지에 0과 1의 난수 스트링인 고정 길이의 MD를 제공
- 이미 다이제스트가 존재하는 메시지가 주어지면 오라클은 저장되어 있는 다이제스트를 제공
- **새로운 메시지에 대한 다이제스트는 다른 모든 다이제스트에 대해 독립적이어야 함**
  - 오라클이 공식이나 알고리즘을 사용해서는 안된다는 것을 의미
- 프리이미지 저항성, 제 2프리이미지 저항성, 충돌 회피성을 가짐

1. `비둘기집 원리(Pigeon-Hole Principle)` : 만약 kn+1마리의 비둘기가 n개의 비둘기집에 들어가 있다면 적어도 한 개의 비둘기집에는 k+1마리의 비둘기가 들어가 있어야 함

2. `생일문제(생일공격)` : 해시값은 뭐든 괜찮으며 어쨌든 같은 해시값을 생성하는 2개의 메시지를 구하는 것
- 강한 충돌 내성을 깨고자하는 공격

### 랜덤 오라클 모델에 대한 공격
- 무차별 공격에 대한 해시함수의 강도는 전적으로 해시코드의 길이에 달려 있음

|구분|공격 난이도|
|:---:|:---:|
|프리이미지 저항성|2<sup>n</sup>|
|제 2프리이미지 저항성|2<sup>n</sup>|
|충돌 저항성|2<sup>n/2</sup>|

## 일방향 해시함수에 대한 공격
1. `무차별 공격`
   - **약한 충돌 내성**을 깨고자 하는 공격
   - 예시 : SHA-1의 경우, 해시값이 160비트이므로 2<sup>160</sup>회를 시행하면 원하는 메시지의 발견을 기대할 수 있음
2. `일치블록 연쇄공격` : M'를 사전에 다양하게 만들어 놓았다가 h(M)과 같은 해시함수값을 갖는 것을 골라 사용하는 공격
3. `중간자 연쇄공격` : 전체 해시값이 아니라 **해시 중간의 결과에 대해 충돌쌍을 찾음**
   - 특정포인트를 공격대상으로 함
4. `고정점 연쇄공격`
   - 고정점 : f(H<sub>i-1</sub>, x<sub>i</sub>) = H<sub>i-1</sub>를 만족하는 쌍 (H<sub>i-1</sub>, x<sub>i</sub>)
   - 메시지 블록과 연쇄변수 쌍을 얻게 되면 연쇄변수가 발생하는 특정한 점에서 임의의 수의 동일한 블록들 x<sub>i</sub>를 메시지 중간에 삽입해도 전체 해시값이 변하지 않음
5. `차분 연쇄공격`
   - 다중 라운드 블록암호의 공격 : 입력값과 대응하는 출력값 차이의 통계적 특성을 조사
   - 해시함수의 공격 : 압축함수의 입출력 차이를 조사하여 0의 충돌쌍을 찾아내는 방법을 주로 사용

## 일방향 해시함수로 해결할 수 없는 문제
- **무결성(조작과 변경)을 확인**할 수는 있지만 **인증(거짓행세)을 확인할 수는 없음**
- **인증을 위해 필요한 기술이 메시지 인증코드와 전자서명**





# [2] 암호학적 해시함수의 예
_____
## SHA-512
### 구조
![SHA-512구조](http://dev-ujin.github.io/assets/res/informational-security/sha512-structure.png)

### 길이필드와 패딩
![SHA-512길이필드와 패딩](http://dev-ujin.github.io/assets/res/informational-security/sha512-length-padding.png)
- 길이필드 : 부호 없는 정수로, 해시값이 같으면서 입력값이 다른 메시지를 찾는 것을 어렵게 함 

### 안전성
- 동일한 MD를 갖는 두 메시지를 찾는데는 2<sup>256</sup>번의 연산을 수행해야할 정도
- SHA-512도 이전의 SHA와 같은 구조로 수학적으로도 동일하게 동작하므로 우려하여 NIST가 SHA-3를 공모함

## SHA-3
- 경쟁방식에 의한 표준화(암호학자끼리 서로 알고리즘을 평가)에 의해 KECCAK이 SHA-3로 결정되어 일방향 해시함수의 새로운 표준이 됨





# [3] 메시지 인증코드(MAC, Message Authentication Code)
_____
## `변경감지코드(MDC, Modification Detection Code)`
- **키가 없는 해시함수**

![MDC](http://dev-ujin.github.io/assets/res/informational-security/mdc.png)

## `메시지인증코드(MAC, Message Authentication Code)`
- **키가 있는 해시함수**

![MAC](http://dev-ujin.github.io/assets/res/informational-security/mac.png)
- 상호 비밀키를 알고 두 코드가 동일한 경우
  1. 무결성 확인 가능 : 만약 공격자가 메시지를 변경했다면 계산된 코드 &#8800; 수신한 코드
  2. 인증 가능 : 다른 사람은 비밀키를 모르고, 정확한 코드를 갖는 메시지를 만들어 낼 수 있음
  3. 메시지가 순서번호를 사용했다면 정확한 순서라는 것을 알 수 있음

## MAC의 키 배송 문제
- 송신자와 수신자가 키를 공유해야하기 때문에 대칭키 암호에서의 키 배송 문제가 여기서도 발생함

## MAC의 구현 사례

### 1. `축소 MAC(Nested MAC)`
- MAC의 안전성을 높이기 위해서 설계

![축소 MAC](http://dev-ujin.github.io/assets/res/informational-security/nested-mac.png)

### 2. `HMAC(Hash MAC)`
- SHA-1과 같이 **일방향 해시함수를 이용**하여 메시지 인증코드를 구성하는 방법
- 사용하는 일방향 해시함수는 여러 종류일 수 있음
- RFC 2104로 출판되었음
- **TLS(Transport Layer Security), IPSec(IP Security), SET(Secure Electronic Transaction)같은 프로토콜에 이용**

### 3. `CBC-MAC, CMAC`
- 대칭키 암호시스템에 대한 암포 블록체인코드(CBC)와 유사한 방법
- 대칭키 암호를 N번 사용하여 N개의 평문블록에서 '하나의' MAC을 생성하는 차이가 있음
- CBC-MAC에서 보안 논점이 발견되어 CMAC(Cipher-based MAC)이 만들어졌음
  - 같은 종류의 데이터 인증과 무결성을 제공하지만 수학적으로는 보다 안전함

### 4. `CCM(Counter with CBC-MAC)`
- CTR과 CBC-MAC을 통합한 모드
- 목적 : 동일한 키의 사용을 통해**기밀성과 인증(무결성)**을 제공
- 핵심 알고리즘 구성요소 : **AES 암호 알고리즘, CTR 운용모드, CBC-MAC 인증 알고리즘**
  - 암호화와 MAC 알고리즘에 **동일한 키 하나가 사용됨**
 
### 5. `GCM모드(Galois/Counter 모드)`
- CTR 모드에 인증 기능을 추가한 모드
- CTR 모드가 암호문을 생성함과 동시에 이 암호문이 올바른 암호화를 거쳐 만들어진 것임을 인증하는 정보(인증자)를 만들어내는 구조
- 적극적 공격자가 암호문을 위조하여 배포해도 위조된 암호문임을 간파할 수 있음

## MAC에 대한 공격
- 재전송 공격 : 단순한 메시지 인증코드는 공격자의 재전송공격을 방지할 수 없음
  - 공격자가 전송 중인 메시지와 메시지 인증코드를 스니핑해 재전송하는 경우

### 1. `순서번호(sequence number)`
- 송신 메시지에 매회 1회씩 증가하는 번호를 붙여 **MAC값의 계산에서도 순서번호를 메시지에 포함시키는 방법**
- 맬로리가 순서 번호를 늘렸을 때의 MAC값을 계산할 수 없게 됨
- **통신 상대마다 마지막 순서번호를 기록해두어야하는 번거로움이 있음**

### 2. `타임스탬프(Timestamp)`
- **송신 메시지에 현재 시각을 넣어**, 그 이전의 메시지가 왔을 경우에는 MAC값이 바르더라도 오류라고 판단
- **송, 수신자 사이에 시계를 일치시켜두는 동기화가 필요**

### 3. `비표(nounce)`
- 메시지 수신에 앞서 **수신자가 송신자에게 일회용 랜덤 값(비표)을 건넴**
- **비표를 포함해 MAC값을 계산**
- **통신 데이터의 양이 약간 증가함**

### 4. `시도/응답(Chanllenge/Response)`
- **B가 A에게 우선 난수(신청)를 송신한 다음, A로부터 송신 이후에 수신되는 메시지(응답)가 정확한 난수값을 포함할 것을 요구함**

## MAC으로 해결할 수 없는 문제

### 1. 제 3자에 의한 증명
- 앨리스와 바이 통신하는 동안에는 'MAC값을 계산하는 것은 상대방'이라고 말할 수 있지만, 빅터에게 'MAC값을 계산한 것은 내가 아닌 상대방'이라고 증명할 방법이 없음
- **전자서명을 사용하면 가능**

### 2. 부인방지(Nonrepudation)
- 앨리스와 밥이 부인을 하면 어느쪽 주장이 맞는지 판단할 수 없기 떄문에 부인방지할 방법이 없음
- **전자서명을 사용하면 가능**