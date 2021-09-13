---
published: true
title: '[컴퓨터 보안] User Authentication'
layout: post
subtitle: 'csReview Computer Security'
categories: csReview
tags: ComputerSecurity
comments: true
---

# User Authentication

### Authentication Process
인증절차를 말하며 제일 기본적이고 1차적인 방어선 역할을 한다. 접근 제어와 user accountability에 대한 기초이다.
+ Identification Step: 보안 시스템에 identifier를 제시하는 과정
+ Verification Step: 유저와 identifier간의 관계를 확인하는 인증 정보를 표시하거나 생성하는 과정

### 4 means of authenticating user identity
1. 개인이 **아는** 것
  ex) 비밀번호, PIN번호, 미리 정해진 질문에 대한 대답 등
2. 개인이 **소유**하는 것
  ex) Smartcard, Electronic keycard, physical key
3. **Static biometrics**와 같이 해당 개인 그 자체임을 알 수 있는 것
  ex) 지문, 망막, 얼굴 등
4. **Dynamic biometrics**와 같이 해당 개인만이 할 수 있는 것
  ex) 목소리 패턴, 글씨체, typing rhythm

### Password Authentication
제일 널리 사용되는 인증 방식으로, 유저는 ID와 PW를 제공하고 시스템은 그를 저장되어 있는 정보와 비교하여 인증하는 방식이다
ID는 사용자가 시스템에 접근 가능한지 여부와 사용자의 권한을 결정하고, 분산 액세스 제어에도 사용이 가능하다.  

### Password Vulnerabilities
패스워드 인증방식은 다음과 같은 8 가지 공격이 가능하다.   
1. Offline dictionary attack
2. Specific account attack
3. Popular password attack
4. Password guessing against single user
5. Workstation hijacking
6. Exploiting user mistakes
7. Exploiting multiple password use
8. Electronic monitoring

### Countermeasures
패스워드 인증방식의 공격에 대한 대응책으로는 아래와 같은 것들이 있다.
+ 암호 파일에 대한 무단 액세스를 방지하는 컨트롤
+ 침입 탐지(Intrusion detection) 방법
+ 손상된 암호의 신속한 재발급
+ 계정 잠금 장치
+ 사용자가 공통된 비밀번호를 선택하지 못하도록 하는 정책
+ 암호 정책 교육 및 시행
+ 9자 이상
+ 대/소문자, 특수 문자 포함 등
+ 자동으로 워크스테이션 로그아웃
+ 네트워크 장치들의 유사한 암호에 대한 정책

### Hashed Passwords(Password Salt)
![Use of Hashed Passwords](https://sundongkim-dev.github.io/assets/img/hashedPW.jpg)

이와 같은 Salt를 사용하면 공격자로 하여금 비밀번호를 찾기 힘들게하고 찾더라도 그저 한 가지 케이스의 비밀번호를 알아냈을 뿐이게 된다. 만약, B가 Salt의 길이이고, D가 사전(Dictionary attack)안의 단어 수라면.. 검색해야 하는 크기는 2<sup>B</sup>*D이다. 32bit Salt에 500,000개의 단어가 사전에 있다면, 2천조가 넘는 검색 크기를 갖는다.

### UNIX Implementation
UNIX에선 원래 최대 8글자로 하위 7비트만 모아서 56비트 DES키를 만든다. 영어 대소문자, 숫자와 ./에서 2글자를 골라 12비트를 정하고, salt에 의해 변형된 DES알고리즘을 이용해 모든 비트가 0인 블록을 25번 암호화한다. 결과물은 11글자로 출력되는데, 현재는 앞선 방식이 느리고, 보안 강도에 있어 8글자가 너무 짧기에 보다 나은 해쉬함수와 길이를 늘리는 식으로 사용한다.
![Improved Implementations](https://sundongkim-dev.github.io/assets/img/improvedImplementations.jpg)

### Password Cracking
+ Dictionary Attacks: 가능한 암호에 대한 큰 사전을 만들고 이를 대입한다. 암호들은 각 솔트 값을 사용하여 해시되어야 하며 저장된 해시 값과 비교한다.  
+ Rainbow Table Attacks: 모든 Salt에 대한 해시값을 저장한 표(rainbow table)를 만들고 크래킹하고자 하는 해시 값을 테이블에서 검색해서 역으로 패스워드를 찾는다. 그러나, Salt 값을 매우 크게 한다면 이러한 공격은 하기 어렵다.

### Password File Access Control
암호화된 암호에 대한 액세스를 거부하여 offline guessing attack을 차단할 수 있다. 오로지 권한이 있는 사용자에게만 사용 가능하게 한다.
+ Shadow password file: 해시 암호가 보관되는 사용자 ID와 별도의 파일

**취약점**
+ 파일 액세스를 허용하는 OS의 취약점
+ 읽기 권한을 부여하는 accident
+ 다른 시스템에도 사용하는 같은 비밀번호
+ 백업 매체에 대한 접근(백업 데이터에 패스워드 파일이 있을 수도 있음)
+ 네트워크 상에서 비밀번호 스니핑

### Password Selection Techniques
1. User education: 사용자들은 비밀번호를 추측하기 어렵게 사용하는 것의 중요성을 알게 하고 강력한 비밀번호를 선택하기 위한 가이드라인을 제공
2. Computer generated passwords: 유저가 외우기 힘듦
3. Reactive password checking: 시스템이 주기적으로 자체적인 PW cracker로 guessable PW를 찾는다
4. **Proactive password checking**: PW를 만들때부터 시스템이 정해 놓은 정책에 부합하는 지 체크해서 부합하지 않는다면 다시 설정하게 한다. Gussable PW를 없애기 위함인 동시에 유저가 외우기 쉬운 것을 암호로 고르게 하기 위함이다

### Proactive Password Checking
+ Password Cracker
+ Rule Enforcement: 암호가 준수해야 하는 특정 규칙
+ Bloom Filter: 집합(사전) 내에 특정 원소(PW)가 존재하는지 확인하는데 사용되는 확률적 자료구조
  + 원소 추가: 추가하려는 원소에 대해서 k개의 해시 값을 계산한 다음, 각 해시 값을 비트 배열의 인덱스로 해서 대응하는 비트를 0이면 1로 바꾼다
  + 원소 검사: 검사하려는 원소에 대해서 k개의 해시 값을 계산한 다음, 각 해시 값을 비트 배열의 인덱스로 해서 대응하는 비트를 읽는다. k개의 비트가 모두 1인 경우 원소는 집합에 속한다고 판단하고, 그렇지 않은 경우 속하지 않는다고 판단한다


### Password Security(Login Scoring)
+ Login Scoring
  + Request Data(IP주소, 타임스탬프, 쿠키 등)
  + Reputation scores
  + Global counters
  + History of member's previous (successful) logins
+ No per-user attack data
