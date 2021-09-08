---
published: true
title: '[컴퓨터 보안] Cryptographic Tools(2)'
layout: post
subtitle: 'csReview Computer Security'
categories: csReview
tags: ComputerSecurity
comments: true
---

### Message Authentication
해시 알고리즘으로 메시지의 수정을 detect할 수 있지만(무결성 확보), 소스가 정확한지 여부(Masquerade)를 속일 수 있기 때문에 이러한 인증이라는 절차가 필요하게 되었다. 또한 수신자와 송신자가 Key를 공유한다.

**Message Authentication Codes(MAC)**
MAC algorithm을 통해 데이터의 무결성과 Authentication을 동시에 제공한다. 메시지와 Key가 Mac algorithm을 통해 나온 MAC을 메시지에 붙여서 전송하고, 수신자는 자신이 가지고 있는 Key로 MAC을 생성하여 수신한 것과 같은 지 비교함으로써 Authentication을 증명한다.

**Secure Hash Functions**
위의 과정에서 해시 함수가 쓰이는데, L bits의 임의의 길이의 메시지가 있다고 하자. 이를 해시 함수의 input으로 하여 나온 결과값을 H라고 한다면 이 h는 input과는 달리 고정된 길이를 갖는다. 이 때, L의 길이가 h의 길이보다 크다면, 다른 메시지에 대해 같은 해시 값을 갖게 된다. 이를 Collision이라고 한다.

이러한 **One-Way Hash Function**을 이용하여 Message Authentication을 하는 방법은 크게 세 가지가 있다.
1. Conventional Encryption
2. Public-key Encryption
3. Secret Value

**Hash Function Requirements**
+ 모든 크기의 데이터 블록에 적용할 수 있다.
+ 고정된 길이의 output을 생성한다.
+ H(x)는 주어진 x에 대해 계산하기 쉽다.
+ H(x)=h를 만족하는 x를 계산하기 어렵다.
+ **Weak collision resistance**: x가 주어졌을 때, H(y)=H(x)를 만족하는 y를 계산하기 어렵다.
+ **Strong collision resistance**: H(x)=H(y)를 만족하는 어떠한 x,y를 계산하기 어렵다.

**Security of Hash Functions**
해시 함수를 공격하는 데 있어서 두 가지 방식이 있다.
1. Cryptanalysis: 알고리즘의 논리적 취약성을 찾아낸다.
2. Brute-force attack: 가능한 모든 경우의 수를 시도해서 답을 알아낸다.(해시 값의 길이에 달려있음)

### Secure Hash Algorithm(SHA)
![Comparision of SHA Parameters](https://sundongkim-dev.github.io/assets/img/SHA.jpg)

**Birthday attack**
이를 알려면 먼저 Birthday paradox에 대해 먼저 알아야 한다. 한 집단에 23명 이상의 사람이 모이면 그 중 생일이 같은 사람이 적어도 한 쌍 이상 있을 확률이 50%를 넘는다는 것이다.(아마도 생각보다 너무 적은 수라 paradox라는 말이 붙지 않았을까 싶다..) 증명 자체는 간단하다. 첫 번째는 365일 중 어떤 날도 선택할 수 있기에 1/365, 두 번째는 1-1/365, 이런 식으로 23명까지 곱하면 0.493이고 이는 서로 생일이 다를 확률을 말한다. 결론적으로 0.507로 50%를 넘는다. 이를 일반화하면 N 개의 가능성이 있다면 최소한 2의 n/2제곱을 조사하면 중복이 나올 확률이 50%가 넘음을 알 수 있다.

### HMAC(Hash-based Message Authentication Code)
![HMAC Structure](https://sundongkim-dev.github.io/assets/img/HMAC.jpg)

---
### Public-Key Encryption Structure
대칭키 암호화를 이용하면 키를 탈취당할 위험도 있고, 사람이 많아질수록 키가 너무 많아져서 관리하기 힘들어진다. 이러한 키의 분배나 디지털 서명에 있어 문제점이 있지만 비대칭키보다 매우 빠르기 때문에 아직도 쓰인다. 즉, 공개 키 암호화라는 비대칭 암호화 방식은 저런 문제점을 해결한 암호화 방식이다. 공개 키 암호화에는 다음 5 가지 요소가 있다.
1. PlainText
2. Encryption algorithm
3. Public and Private key
4. Ciphertext
5. Decryption Key

공개 키 암호 시스템의 요구 사항으로는 다음 5 가지가 있다.
1. Key 쌍을 만들기 쉽다
2. 송신자가 수신자의 Public key를 알기 쉽다
3. 송신자가 private key로 복호화하기 쉽다
4. Public key를 보고 Private key를 계산할 수 없다.
5. 누군가가 암호화된 Message를 보고 Original message로 recover할 수 없다.

---
### Asymmetric Encryption Algorithms
#### RSA(Rivest,Shamir & Adleman)
+ 인수분해의 어려움을 이용한 가장 대표적인 공개 키 암호 알고리즘이다.
+ 암호화: C = M<sup>e</sup> mod n
+ 복호화: M = C<sup>d</sup> mod n = (M<sup>e</sup>)<sup>d</sup> mod n = M
+ 송신자와 수신자 모두 n과 e의 값을 알고 있고, 수신자만이 d 값을 알고 있다.

**n과 e와 d 구하는 방법**
1. n은 임의의 소수 p와 q의 곱이다.
2. 파이 n은 (p-1)*(q-1)이다.
3. e는 1보다 크고 파이 n보다 작으며 파이 n과 서로소인 수로 정한다.
4. e*d mod (파이 n)은 1의 값을 갖는 d를 구한다.

**Security of RSA(공격 방법)**
1. Brute-force
2. Mathematical Attacks
  + 두 개의 소수 곱을 인수분해하는 방법인데 이를 막으려면 매우 긴 길이의 키를 사용해야 하지만, 시스템 처리 속도는 느려진다.
3. Timing Attacks
  + 복호화 알고리즘의 실행 시간에 따라 값을 유추한다. 가령 비트열에서 임의의 위치가 0이라면 cpu는 연산을 하지 않기에 비트열을 추론할 수 있게 된다.
4. Chosen ciphertext attacks
  + 공격자가 위조 암호문을 만들어 보내 서버가 회신해 주는 오류 메시지나 타이밍을 해석하여 정보를 얻어내는 방법

#### Diffie-Hellman Key Exchange
이산 대수 문제를 이용하여 대칭 키를 공유하는 데 사용하는 알고리즘이다. 간단히 말해, 상대의 공개키와 나의 개인키를 이용하여 비밀키를 얻고 그 후 나와 상대방은 그 비밀키를 이용하여 데이터를 암호화하여 통신하면 된다. 과정은 다음과 같다. 흔히 쓰이는 Alice와 Bob을 송신자와 수신자로 하자.
1. Alice와 Bob은 q와 a를 정하는데, q는 소수이고, a는 q보다 작고 q의 원시근이어야 한다.
2. 그 후 Alice는 q보다 작은 X<sub>A</sub>(private)를 정하고, public Y<sub>A</sub>를 계산한다. Y<sub>A</sub>=a<sup>X<sub>A</sub></sup> mod q이다.
3. Bob도 Alice와 마찬가지로 Y<sub>B</sub>를 계산한다.
4. 서로 계산한 Y값을 교환한다.
5. 비밀 키는 얻은 Y값에 자신의 private한 값을 제곱하여 계산한다.

**Man-in-the-Middle Attack(중간자 공격)**이 일어날 수 있는데 이는 최초의 정한 소수 q를 매우 큰 값으로 정한다면 안전하다고 볼 수 있다. 공격자는 Y값만을 가로챌 수 있는데, 이 둘을 곱해봐야 값을 유추하기 어렵기 때문이다.

#### Digital Signature Standard
말 그대로 디지털 서명 알고리즘으로, 소스 및 데이터 무결성 인증에 사용된다. 그러나 Confidentiality를 보장하지 않는다.

#### Elliptic-Curve Cryptography(ECC)
RSA와 비슷한 보안 강도를 지니지만 더 작은 bit size를 갖는다. 타원 곡선 이론에 기반한 암호화 방식이다. 추후에 자세히 알아보자.

**정리**

|Algorithm|Digital Signature|Symmetric Key Distribution|Encryption of Secret Keys|
|---|---|---|---|
|RSA|Yes|Yes|Yes|
|Diffie-Hellman|No|Yes|No|
|DSS|Yes|No|No|
|Elliptic Curve|Yes|Yes|Yes|

---
### Public Key Certificates
공개 키가 조작되었을 수 있기 때문에 위와 같은 기술이 생겼다.

### Key Distribution
대칭 키 암호를 사용하면 키를 상대방에게 보내지 않으면 수신자는 복호화할 수 없는데, 키를 보낼 때 공격자가 이를 가로채면 복호화할 수 있게 되기 때문에 문제가 발생한다. 이를 해결하기 위해 **Key Distribution Center**를 이용한다. KDC는 암호 통신이 필요할 때마다 개인에게 key를 공유한다.
**키 공유 과정**
1. 호스트는 통신을 신청한다.
2. KDC는 session key를 만든다.
3. KDC는 통신하려는 두 호스트들에게 session key를 각 host의 key를 사용하여 암호화해서 나눠준다.
4. 송신자는 자신의 key로 KDC에게 받은 것을 복호화하여 session key를 얻고, 그 session key로 암호화하여 메시지를 보낸다.
5. 수신자도 송신자와 마찬가지로 session key를 얻어 송신자의 메시지를 복호화한다.
6. 통신이 종료되면 session key도 폐기한다.


### Kerberos Protocol
사용자가 특정한 서비스에 접근하거나 서비스가 다른 서비스에 접근 할 때, 인증과 권한에 대한 정보를 관리하고 프로세스에 필요한 여러 기능(ticket 발생, 비밀키-대칭키를 통한 보안)들을 제공해 준다.
![Overview of Kerberos](https://sundongkim-dev.github.io/assets/img/Kerberos.jpg)
1. 사용자 로그인
사용자는 특정 서비스에 접근하기 위해 서비스의 클라이언트를 통해 접근한다. 이 때, 사용자는 ID/PW를 입력하며, 서비스를 제공해주는 서버로 부터 Service Session Key와 Ticket을 얻어야 한다. Authentication Server로 자신을 알리고 티켓을 발급받기 위한 티켓(Ticket-granting ticket, TGT)을 얻어야 한다.

2. TGS(Ticket-Granting Service) 세션키 요청
클라이언트는 서비스를 사용하기 위해 TGS(Ticket-Granting Service)로부터 서비스에 대한 세션키와 티켓을 발급받아야 한다. 이 때 해킹의 위험이 있으므로 ID만을 전달한다.

3. 사용자 정보 확인(사용자 PW 비밀키로 암호화한 TGS세션키, TGT전달)
클라이언트로부터 사용자ID를 전달 받으면 AS(Authentication Server)는 자신의 DB에서 해당 사용자가 있는지 확인하고 존재한다면 저장된 사용자PW의 비밀키를 사용하여 TGS세션키를 암호화하여 사용자에게 전달한다. 사용자ID만을 전달 받았기에 진짜 DB에 기록된 사용자가 맞는지 한 번 더 확인하는 것이다.

4. TGS세션키 획득 및 Authenticator 생성
사용자가 맞다면 TGS세션키를 획득할 것이며, 이것으로 Authenticator를 만든다.

6. Authenticator, TGT 전달
클라이언트는 Ticket Granting Server(TGS)에 Authenticator와 TGT를 전달한다.

7. 사용자 인증 정보 확인 및 Ticket 발급
 TGS는 사용자가 보낸 Authenticator와 TGT를 확인한다. 확인이 되면, Ticket과 Session key를 발급해준다.
8. TGS세션키로 SS세션키 복호화 후 Authenticator 전달
9. 사용자 인증 정보 확인 및 서비스 제공

**Kerberos Realm**
+ 서로 다른 관리 조직 아래 클라이언트와 서버의 네트워크는 일반적으로 서로 다른 영역을 구성한다.
+ 다중 영역인 경우, 그들의 Kerberos 서버는 비밀 키를 공유해야 하고 Kerberos 서버를 신뢰해야 한다.
+ 두 번째 영역의 참여 서버 또한 첫 번째 영역의 Kerberos 서버를 신뢰해야 한다.

---
### Public Key Infrastructure X.509(PKIX)
![X.509 Formats](https://sundongkim-dev.github.io/assets/img/X509.jpg)
![PKIX Architectural Model](https://sundongkim-dev.github.io/assets/img/PKIX.jpg)
#### PKIX Management Functions
1. Registration
2. Initialization
3. Certification
4. Key pair recovery
5. Key pair update
6. Revocation request(인증서 파기: 기간 만료, 새로 발급)
7. Cross Certification

---
### Rotor Machines - Enigma
+ 여러 단계의 Substitution과 Transposition 암호화로 이루어진다.
+ 한 실린더의 출력은 다음 입력에 연결되어 있다.
+ 한 번의 Key stroke에 따라 실린더가 한 칸씩 움직이며 다 돌은 경우 다음 level의 실린더가 움직인다.
