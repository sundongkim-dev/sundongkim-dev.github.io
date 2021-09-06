---
published: false
title: '[컴퓨터 보안] Computer Networks and the Internet'
layout: post
subtitle: 'csReview Computer Network'
categories: csReview
tags: ComputerNetwork
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
**Conventional encryption** 또는 **single-key encryption**이라고도 불리며, 매우 강력한 암호화 알고리즘이 요구되며 송신자와 수신자만이 key를 매우 안전한 방식을 거쳐 가지고 있어야 한다.  
아래의 그림과 같이 대칭적인 구조를 갖고 있어 symmetric encryption이라고 한다.  
![Simplified Model of Symmetric Encryption](https://sundongkim-dev.github.io/assets/img/symmetricEncryption.jpg)

1. **DES(Data Encryption Standard)**
64bit 평문을 56bit key로 64bit 암호문을 생성한다. DES 구조는 Feistel Network의 변형된 형태이다. 그러나 최근 하드웨어의 발달로 56bit 암호 key에 의한 암호화는 쉽게 해독이 가능하여 Double DES, Triple DES가 생겨났다.
2. **Triple DES**
DES와 사용하는 알고리즘 자체는 같으며 다만 이를 3단으로 겹친 암호 알고리즘이다. 168bit 길이의 암호키를 사용하여 brute-force attack으로 부터 안전하다. 또한 64bit의 block size를 사용한다. 그러나, 3단으로 겹치다 보니 느리다.
3. **AES(Advanced Encryption Standard)**
Triple DES가 여러 가지 이유로 더이상 유용하지 않다고 판단하여 AES가 만들어졌다. DES를 3번 사용하기에 속도가 느리며, 블록 크기 또한 여러 가지 분야에서 적합하지 않아서이다.
  + Block size는 128, 192, 256bit가 가능하다
  + Key 길이는 128, 192, 256bit가 가능하며 Block size와는 독립적이다
  + DES는 Feistel구조인 반면 AES는 그렇지 않다.
|Size/Algorithm|DES|Triple DES|AES|
|---|---|---|---|
|Plaintext block size(bits)|64|64|128|
|Ciphertext block size(bits)|64|64|128|
|Key size(bits)|56|112 or 168|128, 192 or 256|


### Attacking Symmetric Encryption
* **Cryptanalytic Attacks**: 알고리즘의 특성을 활용하여 특정 일반 텍스트 또는 사용 중인 키를 추론하며 5 가지 예시가 있다.
  + Ciphertext ONLY
  + Known plaintext
  + Chosen plaintext
  + Chosen ciphertext
  + Chosen text(=Chosen plaintext + Chosen ciphertext)
* **Brute-Force Attack**
