---
layout: post
title: "[정보보안기사]필기::02.암호학 개요"
date: 2020-05-06 05:32:00 0800
categories: 정보보안기사
tags: 정보보안 정보보호일반 암호학
---
> 알기사 교재 - section 02. 암호학 개요

# [1] 암호학의 기본 개념
_____
### 정의
평문을 암호문으로 만들고 특정한 비밀키를 알고 있는 사람만이 다시 평문으로 복원시킬 수 있도록 하는 **암호기술(Cryptography)**과 이를 제3자(도청자)가 해독하는 방법을 분석하는 **암호해독(Cyptanalysis)**에 관하여 연구하는 학문

### 암호에서 사용하는 이름
- `앨리스(Alice)` : 메시지를 전송하는 모델
- `밥(Bob)` : 메시지를 수신하는 모델
- `이브(Eve)` : 소극적인 공격자로 통신을 도청하긴 하지만 메시지를 수정하지는 못함
  - 도청자(Eavesdropper)의 의미
- `맬로리(Mallory)` : 통신 중인 메시지를 수정하고 재전송할 수 있는 능력을 가짐
  - 악의를 가진(Malicious) 공격자를 의미.
- `트렌트(Trent)` : 중립적인 위치에 있는 제3자
  - 중재자(Trusted Arbitrator)를 의미
- `빅터(Victor)` : 의도된 거래나 통신이 실제로 발생했음을 검증할 때 등장
  - 검증자(Verifier)를 의미


### 관련 용어
- `암호화` : 키와 알고리즘을 통해서 평문을 암호문으로 바꾸는 과정
- `복호화` : 키와 알고리즘을 통해서 암호문을 평문으로 바꾸는 과정
- 암호라는 기술을 사용해서 **기밀성(비밀성)을 유지**
- `암호시스템(Cryptosystem)` : 암호화와 복호화를 수행하는 시스템
- `평문(Plaintext)` : 암호화하기 전의 메시지
- `암호문(Ciphertext)` : 암호화한 후의 메시지

### 기호적 표현
- 평문 : **M**이나 **P**(Plaintext)
- 암호문 : **C**(Ciphertext)
- 암호 알고리즘 : **E**(Encryption)
- 복호화 알고리즘 : **D**(Decryption)
- 키 : **K**(Key)
- C = E<sub>k</sub>(P) : 평문 P를 키 K로 암호화하여 암호문 C를 얻음. (**C = E(K, P)**로도 표현할 수 있음.)
- P = D<sub>k</sub>(C) : 암호문 C를 키 K로 복호화하여 평문 P를 얻음. (**P = D(K, C)**로도 표현할 수 있음.)

### 보안 상식
- **비밀 암호 알고리즘을 사용하지 않는다**
    - 암호 알고리즘을 비밀로 해서 보안을 유지하려고 하는 행위를 `숨기는 것에 의한 보안(security by obscurity)`이라고 부름
    - 이러한 행위는 어리석고 위험함. 암호 알고리즘의 구조가 폭로되면 그걸로 끝이기 때문
- **약한 암호는 암호화하지 않는 것보다 위험하다**
    - 가장 큰 이유는 '암호'라고 하는 말로 인해 잘못된 안심을 하고, 그 결과 기밀성이 높은 정보를 소홀하게 취급할 위험이 있기 때문
- **어떤 암호라도 언젠가는 해독된다.**
    - 모든 키를 하나도 빠짐없이 시도해보면 암호문은 언젠가는 반드시 해독됨
    - 암호문이 해독되기까지 들어가는 시간과 암호를 사용하여 지키고 싶은 평문의 가치의 `밸런스(trade-off)`가 중요
- **암호는 보안의 아주 작은 부분이다.**
    - **한 시스템의 강도는 가장 약한 링크의 강도**이기 때문에 모든 링크 부위가 골고루 강해야 해당 시스템의 보안성이 강해짐
    - `사회공학 공격(Social Engineering Attack)`
        - 가장 약한 링크는 암호가 아니라 사람
        - `피싱(Phishing)` : 개인정보(Private Data)와 낚는다(Fishing)의 합성어로, 불특정 다수에게 메일을 발송해 위장된 홈페이지로 접속하게 한 뒤 이용자들의 금융정보 등을 빼내는 신종사기 수법
        - `트로이목마(Trojan Horse)` : 컴퓨터 시스템에서 정상적인 기능을 하는 프로그램을 가장해 다른 프로그램 안에 숨어 있다가 그 프로그램이 실행될 때 자신을 활성화하는 악성 프로그램
        - `키로거 공격(Key Logger Attack)` : 사용자의 키보드 움직임을 탐지해 ID나 패스워드, 계좌번호, 카드번호 등과 같은 개인의 중요한 정보를 몰래 빼 가는 해킹 공격.             
- 좋은 암호방식은 암호화와 복호화는 쉽고 빠르지만 해독은 어려운 시스템이라고 할 수 있음





# [2] 암호기법의 분류
_____
## 치환 암호와 전치 암호
- `치환 암호(대치 암호, Substitution Cipher)` : 평문의 문자를 **다른 문자로 교환하는 규칙**
  - **일대일 대응일 필요가 없음**
- `전치 암호(Transposition Cipher)` : 문자 집합 **내부에서 자리를 바꾸는 규칙**
  - **일대일 대응 규칙을 가짐**
   
## 블록 암호와 스트림 암호
- `블록 암호(Block Cipher)` : 어느 **특정 비트 수의 집합을 한 번에 처리**하는 암호 알고리즘
  - **블록 길이(Block Length)**는 **블록의 비트 수**로 일반적으로 **8비트(ASCII)** 또는 ****16비트(Unicode)**
  - 스트림 암호와는 다르게 **Round를 사용**하고, **반복적으로 암호화 과정을 수행**해 암호화 강도를 높임
  - 암호화 방법 : 평문을 일정한 크기의 블록으로 잘라낸 후 암호화 알고리즘을 적용
- `스트림 암호(Stream Cipher)` : 한번에 1비트 혹은 1바이트의 **데이터 흐름(스트림)을 순차적으로 처리**해가는 암호 알고리즘
  - 데이터 흐름을 순차적으로 처리해가기 때문에 **내부 상태**를 가지고 있음
  - **군사 및 외교용**으로 널리 사용되며, 이동 통신 등의 **무선 데이터 보호**에 적합
  - 암호화 방법 : 평문과 키 스트림을 XOR하여 생성

|구분|블록 암호|스트림 암호|
|---|---|---|
|장점|높은 확산, 기밀성, 해시함수|암호화 속도가 빠름, 에러 전파현상 없음|
|단점|느린 암호화, 에러 전달|낮은 확산|
|사례|DES, IDEA, SEED, RC5, AES|LFSR, MUX generator|
|암호화단위|블록|비트|
|주요 대상|음성, 오디오, 비디오 스트리밍|일반 데이터 전송, 스토리지 저장|

- `선형 되먹임 시프트 레지스터(LFSR, Lineer Feedback Shift Register)` : 클럭의 주기에 맞추어 여러 개의 시프트 레지스터 내용이 하나씩 시프트되고, 동시에 출력 값과 시프트 레지스터의 배타적 논리 연산(exclusive OR)값이 시프트 레지스터의 입력으로 인가되는 회로
  - 의사랜덤 시퀀스를 생성하거나 암호 등의 회로에 응용

## 링크 암호와와 종단간 암호화
- `링크 암호화(Link Encryption)` : **모든 정보가 암호화**되고 각 **홉(hop)**에서 해독되어 진행 방향으로 보냄.
  - 라우터는 **패킷의 헤더 부분을 해독**하고, 헤더 내의 라우팅과 주소 정보를 읽고 다시 암호화
- `종단간 암호화(End-to-End Encryption)` : 헤더와 트레일러는 암호화되지 않아 각 홉에서 해독하고 암호화할 필요가 없는 방식.
  - 중간 장비들은 단지 라우팅 정보만 읽어 패킷을 진행방향으로 통과시킴
  - **근원지 컴퓨터 사용자**에 의해 시작됨 -> 메시지 암호에 대한 결정권 -> 유연성

<table>
<thead><tr><th id="one">구분</th><th id="two">링크 암호화</th><th>종단간 암호화</th></tr></thead>
<tbody>
<tr><td>발생 계층</td><td>데이터 링크 혹은 물리적 계층</td><td>애플리케이션 계층</td></tr>
<tr><td>암호화 주체</td><td>ISP나 통신업자</td><td>사용자</td></tr>
<tr><td>장점</td><td>User-transparent하게 암호화되므로 운영이 간단, 트래픽분석을 어렵게 함, 온라인으로 암호화</td><td>사용자 인증 등 높은 수준의 보안 서비스를 제공 가능, 중간노드에서도 데이터가 암호문으로 존재</td></tr>
<tr><td>단점</td><td>중간 노드에서 데이터가 평문으로 노출, 다양한 보안서비스를 제공하는데 한계, 모든 노드가 암호화 장비를 갖추어야하므로 네트워크가 커지면 비용 과다</td><td>트래픽분석에 취약, 오프라인으로 암호화</td></tr>
</tbody>
</table>

## 하드웨어 암호시스템과 소프트웨어 암호시스템
- `하드웨어 암호시스템`
  - 컴퓨터와 통신기기의 내부버스와 외부 인터페이스에 전용 암호처리용 하드웨어를 설치하여 데이터를 암호화
  - CPU에 부담을 주지 않고 빠른 속도로 암호화가 가능

- `소프트웨어 암호시스템`
  - 암호처리용 소프트웨어를 사용한 데이터를 암호화
  - 비용이 저렴
  - 최근 CPU는 처리 속도가 빨라져 소프트웨어에 의한 암호화를 행해도 처리 속도가 문제가 되지 않아 많이 사용

## 기타
- 거부적 암호화(Denial Encryption) : 하나의 암호 테스트를 둘 이상의 방법으로 해독
    - 제 3자에게 가짜 키를 제공하여 가짜 평문을 복호화하도록 하여 비밀성을 보장




# [3] 주요 암호기술에 대한 개괄
_____
- `대칭키 암호` : **암호화할 때 사용하는 키와 복호화할 때 사용하는 키가 동일**한 암호 알고리즘 방식
- `비대칭키 암호` : **암호화할 때 사용하는 키와 복호화할 때 사용하는 키가 다른** 암호 알고리즘 방식
  - 송,수신자 모두 자신만의 한 쌍의 키를 가지고 있어야 함
- `하이브리드 암호 시스템` : **대칭키 암호와 공개키 암호의 장점**을 조합한 암호 방식
- `일방향 해시함수(one-way hash function)`
  - 해시값 : 일방향 해시함수를 사용하여 계산한 값
  - 문서의 **무결성(완전성)**을 확인할 수 있음
- `메시지 인증코드(message authentication code)`
  - 메시지가 생각했던 통신 상대로부터 온 것임을 확인할 수 있음
  - **무결성**(메시지가 전송 도중에 변경되지 않음)과 **인증**(생각했던 통신 상대로부터 온 것임을 확인)을 제공
- `전자서명` : 도장이나 종이 위의 서명을 온라인 세계에 적용한 것
  - **무결성**을 확인하고, **인증**과 **부인방지**를 하기 위한 암호 기술
  - 거짓행세(spoofing), 변경, 부인이라는 위협을 방지할 수 있음
- `의사난수 생성기(PRNG, pseudo random number generator)` : 난수열을 생성하는 알고리즘
  - 키 생성에 사용됨





# [4] 암호분석(암호해독)
_____
## 암호 해독(cryptanalysis)
- `암호 해독` : 암호 방식의 정규 참여자가 아닌 제3자가 암호문으로부터 평문을 찾으려는 시도
- 암호 해독에 참여하는 사람 : 암호해독자, 제3자, 침해자
- 암호문으로부터 평문이나 키를 찾아냄
- `케르히호프의 원리(Kerckhoff's principle)` : 암호시스템의 안전성은 암호 알고리즘의 비밀이 아닌 키의 비밀을 지키는데 의존되어야 한다는 원리

### 종류
1. `암호문 단독 공격(COA, Ciphertext Only Attack)` : 암호해독자가 단지 C를 가지고 P나 K를 찾아내는 방법
   - 암호해독자에게는 가장 불리한 방법
2. `기지 평문 공격(KPA, Known Plaintext Attack)` : 암호해독자는 일정량의 C와 P의 쌍을 알고 있는 상태에서 둘의 관계를 통해 P나 K를 추정하여 해독하는 방법
3. `선택 평문 공격(CPA, Chosen Plaintext Attack)` : 암호해독자가 선택한 P에 대해 C를 얻어 P나 K를 추정하여 암호를 해독하는 방법
   - 공격자가 암호기에 접근할 수 있을 때 사용이 가능
4. `선택 암호문 공격(CCA, Chosen Ciphertext Attack)` : 암호해독자가 선택한 C에 대해 P를 얻어 암호를 해독하는 방법
   - 공격자가 암호 복호기에 접근할 수 있을 때 사용이 가능.
   - `복호 오라클(Decryption Oracle)` : 선택된 암호문을 복화할 수 있는 능력을 갖춘 기계
   - 이 공격에 견딜 수 있는 암호 알고리즘은 강한 알고리즘이라 할 수 있음
   - `고무호스 암호분석(Rubber-Hose Cryptanalysis)` : 암호분석가가 키를 가진 사람을 공갈, 협박, 고문하여 키를 얻어내는 방법으로, 가장 강력한 공격.  

- 암호문 단독 공격, 기지 평문 공격, 선택 평문 공격의 순서로 공격자의 능력이 향상되는 것을 알 수 있음
- 높은 단계의 공격자에게 안전한 암호 방식을 설계하는 것이 일반적인 암호 설계의 방향임





# [5] 암호 알고리즘의 안전성 평가
_____
### 안전성 개념
1. `계산적으로 안전` : 암호시스템을 공격하기 위한 **계산량이 매우 커 현실적으로 공격할 수 없는 경우**
2. `무조건적으로 안전` : 무한한 계산능력이 있어도 공격할 수 없는 경우. 아래 기준 중 최소 하나를 만족
    1. **암호 해독 비용 > 암호화된 정보의 가치**
    2. **암호 해독 시간 > 정보의 유효 기간**
- `워크팩터(Work Factor)` : 공격자가 암호화 방법을 깨는데 걸리는 노력(리소스)

## 암호기술 평가
1. `암호 알고리즘 평가` : 암호 알고리즘에 대한 안정성 평가
    - 제품이나 시스템과 **독립적으로 알고리즘 자체만을 평가**
    - FIPS 197
    - CAVP(Cryptographic Algorithm Validation Program) : 암호 알고리즘 평가 프로그램
2. `암호모듈 평가` : 암호 알고리즘을 이용하여 제공되는 **암호서비스**(기밀성 기능 모듈, 무결성 기능 모듈)에 대한 안전성 평가
    - FIPS 140-2
    - `CMVP(Cryptographic Module Validation Program)` : 암호 모듈의 안전성 검증을 위한 프로그램. 
      - 아래의 세 가지 항목으로 크게 나누어 평가
          - 암호기술의 기술 구현 적합성 평가
          - 암호키 운용 및 관리
          - 물리적 보안
3. `정보보호제품 평가` : **암호모듈을 탑재한 정보보호 제품**(예: 침입차단시스템, 침입탐지시스템)에 대한 안정성을 평가
    - `CC(Common Criteria)`
    - V&V(Validation&Verification) : 소프트웨어 시스템이 사양과 목적을 만족시키는가를 평가하고 검사하는 과정
4. `응용시스템 평가` : 각 제품을 **상호 연동하여 구성되는 시스템**(예: 국가기관망의 네트워크에 대한 보안성 평가, 항공관제센터의 안전성 평가)에 대한 안전성 평가

- 안전성 평가는 응용시스템의 안전성을 평가하는 것이 가장 바람직하나, 이를 개별적으로 평가하기가 상당히 어려움
- **위의 순서대로 평가가 이루어지는 것이 바람직함**





# [6] 지적 재산권 보호
_____
## 스테가노그래피, 디지털워터마킹, 핑거프린팅
- `스테가노그래피(Steganography)` : **전달하려는 기밀 정보를** 이미지 파일이나 MP3 파일 등에 **암호화해 숨기는 심층암호기술**
  - **암호화는 메시지의 내용을 은폐**하고, **스테가노그래피는 메시지 자체를 은폐**
  - 일반적으로 사진파일에 인간이 인지하지 못할 정도로 미세한 변화를 주어 정보를 입력하는 방식
  - 테러리스트들이 비밀연락책(dead-drop)으로 사용하며, 오사마 빈 라덴도 이를 사용하였음

- `디지털 워터마킹(Digital Watermarking)`
  1. `강한(강성) 워터마킹` : 공격을 받아도 쉽게 파괴되거나 손상을 입지 않음
      - 원본의 내용을 왜곡하지 않는 범위 내에서 혹은 사용자가 인식하지 못하도록 저작권 정보를 디지털 컨텐츠에 삽입
  2. `약한(연성) 워터마킹` : 공격을 받으면 쉽게 파괴되거나 손상을 입음
      - 원본 훼손시 삽입된 워터마크가 훼손되어 검출되지 않도록 하여 원본 컨텐츠의 무결성을 보장

- `핑거프린팅(Fingerprinting)` : 디지털 컨텐츠에 구매자의 정보를 삽입하여 불법 배포 발견 시 최초의 배포자를 추적할 수 있게 하는 기술
  - 데이터에 대해 삽입되는 마크의 내용이 달라 동일한 데이터 각각을 식별할 수 있음
  - 소유자 정보와 구매자 정보를 함께 기록

|항목|스테가노그래피|워터마크|핑거프린트|
|---|---|---|---|
|은닉정보|메시지|판매자 정보|구매자 추적정보|
|목적|은닉메시지 검출|저작권 표시|구매자 추적|
|트래킹|불가|가능|가능|
|불법예방 효과|하|중|상|
|저작권증명 효과|하|중|상|
|공격 강인성|상대적 약함|상대적 강함|상대적 강함|

## 디지털 저작권 관리(DRM, Digital Rights Management)
### 개념
- `디지털 저작권 관리(DRM, Digital Rights Management)` : 소유자 혹은 위임자가 지정하는 다양한 방식으로 제어할 수 있게 하는 기술적인 방법
  - DRM이 제어하는 컨텐츠 접근은 실행, 보기, 복제, 출력, 변경 등을 포함
  - DRM이 제어하는 디지털 컨텐츠는 오디오, 비디오, 이미지, 텍스트, 멀티미디어, 컴퓨터 소프트웨어 등을 포함

### 구성 요소
1. `메타데이터(Metadata)` : 컨텐츠 생명주기 범위 내에서 관리되어야 할 **각종 데이터의 구조 및 정보**
2. `패키저(Packager)` : **컨텐츠와 메타데이터**를 Secure Container 포맷으로 **패키징하는 모듈**
3. `시큐어 컨테이너(Secure Container)` : DRM의 보호 범위 내에서 유통되는 **컨텐츠의 배포 단위**
4. `식별자(Identifier)` : 컨텐츠를 식별하기 위한 식별자
5. `DRM 제어기(DRM Controller)` : 사용자의 디바이스에서 컨텐츠가 지속적으로 보호될 수 있도록 **프로세스를 제어**

### 모델
![DRM모델](http://dev-ujin.github.io/assets/res/informational-security/drm-model.png)
- `권리표현언어(REL, Rights Expression Language)` : **컨텐츠 사용 규칙을 표현하는 언어**
  - ODRL(Open Digital Rights Language)
  - MPEG(Moving Picture Expert Group)
    - MPEG-21 DII(Digital Item Identification)
  
### DRM 기술의 예
- `PKI 기반의 불법복제 방지기술` : **컨텐츠를 소비자의 암호화 키**로 패키징해 다른 사람들이 이용할 수 없도록 함
   - 단점 : 소비자 종속 암호화 -> 컨텐츠 배포 서버의 **프로세스 부담이 가중**되고, **슈퍼 배포자와 같은 기능이 없어 디지털컨텐츠 유통에 부적합**
- `DOI 기반의 저작권 보호기술` : 저작권 관리 정보를 바탕으로 **저작권 인증을 부여하는 기술**
   - `DOI(Digital Object Identifier)` : 인터넷주소가 변경되더라도 그 문서의 새로운 주소로 찾아갈 수 있도록 인터넷 문서에 영구적으로 부여된 식별자 IP
   - 단점 : 불법복제, 사용 기능이 제공되지 않아 **적극적인 저작권 보호는 불가능**
 - INDECS(INteroperability of Data Electronic Commerce System) : 전자상거래 트랜잭션에 대한 투명한 정보제공과 디지털 컨텐츠 저작권 보호를 목적으로 하는 저작권 보호 framework
