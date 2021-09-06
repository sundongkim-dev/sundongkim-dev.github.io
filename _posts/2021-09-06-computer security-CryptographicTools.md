---
published: true
title: '[컴퓨터 보안] Cryptographic Tools'
layout: post
subtitle: 'csReview Computer Security'
categories: csReview
tags: ComputerSecurity
comments: true
---

# 컴퓨터 보안 복습
두 번째 수업인데, 실습이 따로 없어서 그런지 이론은 무척이나 재미있다. 컴퓨터를 조금 더 일찍 접했더라면 해커의 삶도 재밌지 않았을까..

## Cryptographic Tools
1. Symmetric Encryption
2. Message Confidentiality
3. Secure Hash Function
4. Public Key Encryption
5. Kerberos

### Symmetric Encryption
* **Conventional encryption** 또는 **single-key encryption**이라고도 불리며, 매우 강력한 암호화 알고리즘이 요구되며 송신자와 수신자만이 key를 매우 안전한 방식을 거쳐 가지고 있어야 한다.  
* 아래의 그림과 같이 대칭적인 구조를 갖고 있어 symmetric encryption이라고 한다.
* Plaintext, Encryption algorithm, Secret key, Ciphertext, Decryption algorithm으로 이루어져있다.
![Simplified Model of Symmetric Encryption](https://sundongkim-dev.github.io/assets/img/symmetricEncryption.jpg)

Symmetric Encryption이기도 하며 Block Cipher Structure를 지닌 다음 3 가지 알고리즘을 정리하겠다. 먼저 Block Cipher Structure에 대해 알아보자.

### **(Symmetric) Block Cipher Structure**
이는 Round(Substitution, Permutation)라는 암호화 단계를 여러 번 수행한다.

### Feistel Cipher Structure
![Feistel Network](https://sundongkim-dev.github.io/assets/img/feistelNetwork.jpg)

|Size/Algorithm|DES|Triple DES|AES|
|---|---|---|---|
|Plaintext block size(bits)|64|64|128|
|Ciphertext block size(bits)|64|64|128|
|Key size(bits)|56|112 or 168|128, 192 or 256|

1. **DES(Data Encryption Standard)**
64bit 평문을 56bit key로 64bit 암호문을 생성한다. DES 구조는 Feistel Network의 변형된 형태이다. 그러나 최근 하드웨어의 발달로 56bit 암호 key에 의한 암호화는 쉽게 해독이 가능하여 Double DES, Triple DES가 생겨났다.
2. **Triple DES**
DES와 사용하는 알고리즘 자체는 같으며 다만 이를 3단으로 겹친 암호 알고리즘이다. 168bit 길이의 암호키를 사용하여 brute-force attack으로 부터 안전하다. 또한 64bit의 block size를 사용한다. 그러나, 3단으로 겹치다 보니 느리다.
![Triple DES(3DES)](https://sundongkim-dev.github.io/assets/img/3DES.jpg)
3. **AES(Advanced Encryption Standard)**
Triple DES가 여러 가지 이유로 더이상 유용하지 않다고 판단하여 AES가 만들어졌다. DES를 3번 사용하기에 속도가 느리며, 블록 크기 또한 여러 가지 분야에서 적합하지 않아서이다.
  + Block size는 128, 192, 256bit가 가능하다
  + Key 길이는 128, 192, 256bit가 가능하며 Block size와는 독립적이다
  + DES는 Feistel구조인 반면 AES는 그렇지 않다.
![AES](https://sundongkim-dev.github.io/assets/img/AES.jpg)
![AES Rounds](https://sundongkim-dev.github.io/assets/img/AES_EncryptionRounds.jpg)

**AES에 사용되는 각종 연산들**
1. **SubBytes**: S-box를 통해 바이트 단위로 업데이트한다
2. **Shift Rows**: 각 행에 따라 행의 단위만큼 이동한다. 즉, row-1만큼 이동함
3. **Mix Columns**: 각 열들이 고정된 다항식에 의해 치환된다.
4. **Add round key**: Mix Columns의 출력과 라운드 키의 XOR값을 구한다.

### Modes of Operation(in Symmetric Block Encryption)
1. **ECB(Electronic Codebook)**
ECB모드가 가장 단순한 모드로, 한번 암호화 할 때 64bit 블록 단위로 진행하며, 동일한 블록이 입력되면 암호문도 동일하다. 그렇기에 공격자에 의해 한 개의 블록만 해독되면 모든 Round가 동일한 Key를 지니기에 나머지 블록도 해독이 된다.  
2. **CBC(Cipher Block Chaining)**
ECB의 단점을 해결한 것으로, 동일한 블록이어도 다른 암호문 블록을 생성한다. 평문의 각 블록은 XOR연산을 통해 이전 암호문과 연산하는 **연쇄**적인 구조이다. 첫 번째 암호문에 대해서는 IV(Initial Vector)가 암호문 대신 사용된다. 암호문이 블록의 배수가 되기 때문에 복호화 후 평문을 얻기 위해서는 Padding을 해야만 한다.
![CBC](https://sundongkim-dev.github.io/assets/img/CBC.jpg)
3. **CFB(Cipher Feedback)**
블록 암호화를 스트림 암호화처럼 구성하여 평문과 암호문의 길이가 같아져 Padding이 필요 없다. CBC와 마찬가지로 IV가 최초의 암호문 블록 생성을 도와준다.  
4. **OFB(Output Feedback)**

5. **CTR(Counter)**
카운터(블록을 암호화할때마다 1씩 증가)를 암호화한 비트열과 평문블록과의 XOR를 취한 결과가 암호문 블록이 된다.

### Cryptography
암호학에 있어 세 가지 차원에 따라 분류할 수 있다.
1. 평문에서 암호문으로 바꾸는 데 어떤 작업을 하는가?
  + Substitution(치환)
  + Transposition(전치)
2. 몇 개의 Key가 사용되는가?
  + 한 개라면 Symmetric
  + 서로 다른 Key를 사용한다면 Asymmetric
3. 얼마만큼을 평문을 처리할 것인가?
  + Block cipher: 블록 단위로 처리함
  + Stream cipher: 데이터 스트림을 순차적으로 처리(1 bit씩)

### Attacking Symmetric Encryption
* **Cryptanalytic Attacks**: 알고리즘의 특성을 활용하여 특정 일반 텍스트 또는 사용 중인 키를 추론하며 5 가지 예시가 있다.

  + Ciphertext ONLY: 공격자는 사용된 암호 알고리즘을 알고 있는 채로, 암호화된 문서를 가로채 공격하는 방식이다.
  + Known plaintext: Ciphertext-only에 더해 공격자가  plainText와 cipherText를 가지고 있어서 이 쌍을 이용해 앞선 방식 보다 key를 더 쉽게 추측할 수 있다.
  + Chosen plaintext: 공격자가 원하는 새로운 plainText를 만들어 cipherText를 만들어 낸 뒤에 이를 분석하여 key를 추측한다.
  + Chosen ciphertext: 공격자는 가로챈 cipherText의 일부를 이용하여 새로운 cipherText를 만들며, 이를 plainText로 만들어 낸 뒤에 이를 분석하여 사용된 key를 추측한다.
  + Chosen text(=Chosen plaintext + Chosen ciphertext)
* **Brute-Force Attack**: 가능한 모든 경우의 수를 대입하여 공격하는 방법이다.

### Block Cipher Structure
