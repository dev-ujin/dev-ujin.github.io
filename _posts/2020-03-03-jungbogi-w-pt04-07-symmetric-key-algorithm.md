---
layout: post
title:  "[정보보안기사/필기/Part04]07. 대칭키 암호"
date:   2020-03-03 03:32:00 0800
categories: 정보보안기사
tags: 정보보안 정보보호일반 대칭키 암호
---
> 2020 알기사 정보보안기사 `section 03. 대칭키 암호`를 공부한 내용을 바탕으로 작성하였습니다.

##### 현대 블록 암호
- 확산과 혼돈과 같은 성질을 만족시키기 위해 전치 요소(P-box)와 치환 요소(S-box) 그리고 그 밖의 구성요소들을 결합하여 설계.
- 공격 방지 암호를 제공하기 위해 **이동(shift)요소, 교환(swap)요소, 분할(split)요소, 조합(combine)요소**뿐만 아니라 **전치 장치(transposition, P-box), 치환 장치(substitution, S-box), XOR연산(exclusive-OR)**의 조합으로 만들어짐.

##### P-박스(P-box)
- 문자 단위로 암호화를 수해하였던 고전 전치 암호를 병렬적으로 수행.
- P-박스 종류
    - 단순(straight) P-박스
        - 역함수가 존재함.
    - 축소(compression) P-박스 : n비트를 입력받아 m비트를 출력하는 P-박스로서 n > m을 만족.
    - 확장(expansion) P-박스 : n비트를 입력받아 m비트를 출력하는 P-박스로서 n < m을 만족.
        - 비트를 치환하고 동시에 다음 단계에서 비트의 양을 증가시키고자 할 때 사용.
    
##### S-박스(S-box)
- n비트를 입력받아 m비트를 출력한다고 할 때, n과 m이 같을 필요 없음.
- n과 m이 같을 때에만 역함수가 존재함.
- S-박스 구성요소
    - 치환요소(substitution)
    - XOR(exclusive-OR)
    - 이동요소(shift)
    - 교환요소(swap)
    - 분할요소(split)
    - 조합요소(combine)

##### 합성 암호(Product Ciphers)
- `합성 암호` : 치환, 전치 그리고 그 밖의 구성요소들을 결합한 복합적인 암호.
- 확산과 혼돈의 성질을 갖도록 설계.
    - **확산(diffusion)** : 암호문과 평문 사이의 관계를 숨기는 것. 암호문에 대한 통계 테스트를 통하여 평문을 찾고자 하는 공격자를 좌절시킴.
    - **혼돈(confusion)** : 암호문과 키의 관계를 숨기는 것. 암호문을 이용하여 키를 찾고자 하는 공격자를 좌절시킴. 즉, 키의 단일 비트가 변하면 암호문의 거의 모든 비트가 변함.
- **라운드(Rounds)** : 반복적으로 사용되는 합성 암호.
- **양자 암호학** : 양자역학의 원리를 응용한 암호방식. 도청을 수행하면 정보의 내용이 변해버려 쓸모없어지게 하는 것.
- Feistel 암호와 SPN구조가 합성 암호에 속함.

##### Feistel 암호
- 페이스텔 구조에서 네트워크라는 이름은 구성도가 그물을 짜는 것과 같이 교환되는 형태로 구성되어 있기 때문에 붙여진 것.
- 암호 강도를 결정짓는 요소는 평문 블록의 길이, 키 K의 길이, 라운드의 수. 안전성을 보장받기 위해서는
    - 평문 블록의 길이는 64비트 이상.
    - 키 K의 길이는 64비트 내외. 최근에는 128비트를 권장.
    - 라운드 수는 16회 이상.
- 복호화 과정은 암호화 과정과 동일. 입력은 암호문과 보조키 K<sub>i</sub>이며 보조키의 순서는 암호화 과정의 반대로 K<sub>n-1</sub>부터 K<sub>1</sub>.
- 라운드 함수를 F, 라운드키를 K<sub>i</sub>라 할 때, i번째 라운드 과정은
    - L<sub>i</sub> = R<sub>i-1<sub>
    - R<sub>i</sub> = L<sub>i-1</sub> &oplus; F<sub>i</sub>(R<sub>i-1</sub>, K<sub>i</sub>)
    - 최종 라운드에서는 좌우 블록을 한 번 더 교환해야함.
- 장점 : 알고리즘의 수행속도가 빠르고, 하드웨어 및 소프트웨어의 구현이 용이하고, 아직 구조상에 문제점이 발견되고 있지 않음.
![Feistel 구조](https://dev-ujin.github.io/assets/res/feistel_structure.png){: .center}

##### SPN(Substitution-Permutation Network) 구조
- '여러 개의 함수를 중첩하면 개별 함수로 이루어진 암호보다 안전하다'는 Shannon의 이론에 근거해 치환 암호와 전치 암호를 중첩하는 형태로 개발한 암호.
- 입력을 여러 개의 소블록으로 나누고 각 소블록을 S-box로 입력하여 대치시키고, 그 출력을 P-box로 전치하는 과정을 반복하는 방식.
![SPN 구조](https://dev-ujin.github.io/assets/res/spn_structure.png){: .center}

##### 블록 암호에 대한 공격
1. `차분 분석(차분 해독법, Differential Cryptanalsis)`
   - '평문의 일부를 변경하면 암호문이 어떻게 변화하는가?'를 조사하는 암호 해독법.
   - 블록 암호에서는 평문이 한 비트라도 달라지면 암호문은 전혀 다른 비트 패턴으로 변화하는데, 이 암호문의 변화 형태를 조사하여 해독하는 것.
2. `선형 분석(선형 해독법, Linear Cryptanalysis)`
   - '평문과 암호문 비트를 몇 개 정도 XOR해서 0이 되는 확률을 조사'하는 해독 방법. 마츠이가 개발.
   - 암호문이 충분히 랜덤하게 되어 있으면, 평문과 암호문의 비트를 몇 개 XOR한 결과가 0이 되는 확률은 1/2일 것이므로 1/2에서 크게 벗어나는 비트의 갯수를 조사하여 키에 관한 정보를 얻는 것.
3. `전수공격법(Exhaustive Key Search)`
   - 암호화할 때 일어날 수 있는 가능한 모든 경우에 대하여 조사하는 방법. Diffie와 Hellman이 제안.
   - 경우의 수가 많은 경우에는 실현 불가능한 방법.
4. `통계적 분석(Statistical Analysis)`
   - 알려진 모든 통계적인 자료를 이용하여 해독하는 방법.
5. `수학적 분석(Mathematical Analysis)`
   - 통계적인 방법을 포함하며 수학적 이론을 이용하여 해독하는 방법.

##### 참고
1. Feistel 구조 : <https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%9D%B4%EC%8A%A4%ED%85%94_%EC%95%94%ED%98%B8>
2. SPN 구조 : <https://en.wikipedia.org/wiki/Substitution%E2%80%93permutation_network>

<style>.center {display: block;margin: auto;align: center;width: 50%;height: 40%;}</style>