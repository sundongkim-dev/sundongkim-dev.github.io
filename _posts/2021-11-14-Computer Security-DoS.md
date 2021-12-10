---
published: true
title: '[컴퓨터 보안] Denial Of Service Attacks'
layout: post
subtitle: 'csReview Computer Security'
categories: csReview
tags: ComputerSecurity
comments: true
---

# Denial-Of-Service(DoS) Attack
DoS 공격이란 CPU, 메모리, 대역폭 및 디스크 공간과 같은 리소스를 소진하여 네트워크, 시스템 또는 애플리케이션의 인증된 사용을 방지하거나 저해하는 것을 말한다.

- 어떤 서비스의 이용에 대한 일종의 공격
공격 가능한 리소스 범주는 다음과 같다.
1. **Network bandwidth**
서버에 인터넷을 연결하는 네트워크 링크의 용량과 관련되며
대부분의 조직에서 ISP(인터넷 서비스 공급자)에 대한 연결을 말한다.
2. **System resources**
네트워크 처리 소프트웨어에 overload 또는 crash를 목표로 한다.
3. **Application resources**
일반적으로 많은 유효한 요청을 포함하며, 각 요청은 상당한 리소스를 소비하므로 다른 사용자의 요청에 응답하는 서버의 능력을 제한할 수 있다.

## Classic Denial-of-Service Attacks
**Flooding ping command**
네트워크가 정상적으로 작동하는지 여부를 확인하기 위해 사용하는 ping test를 공격자가 해킹을 하기 위한 대상 컴퓨터를 확인하기 위한 방법으로 사용하며, 대상 system에 ICMP packet을 계속 보내서 대상 system이 계속적인 Request에 응답하느라 다른 일을 하지 못하게 한다. 또한 네트워크 연결의 용량을 overwhelm하는 것이다.
- 트래픽은 경로의 대용량 링크에 의해 처리될 수 있지만 링크의 용량이 감소하면 패킷이 삭제된다.
- 스푸핑된 주소를 사용하지 않는 한 공격의 근원은 명확하게 식별된다.
- 네트워크 성능이 눈에 띄게 저하된다.

## Source Address Spoofing
- 위조된 source address를 사용한다.
  - 일반적으로 OS의 raw socket interface를 통해서 공격 시스템을 식별하기 어렵다.
- 공격자는 자신의 주소를 target 시스템의 주소로 바꿔서 대량의 패킷을 생성합니다.
- congestion(혼잡)은 라우터가 최종 저용량 링크에 연결되는 결과를 초래할 것이다.
- 네트워크 엔지니어가 라우터의 flow info.를 구체적으로 쿼리할 것을 요구한다.
- backscatter traffic
  - 백스캐터(backscatter)는 스푸핑된 서비스 거부 공격에서 target system의 응답 패킷을 말한다.
  - 공격자가 소스 주소를 임의로 스푸핑하는 경우 공격 대상자의 백스캐터 응답 패킷이 임의 대상으로 다시 전송된다.

## SYN Spoofing
- 일반적인 DoS 공격으로 시스템 리소스, 특히 운영 체제의 네트워크 처리 코드에 대한 공격이다.
- 서버가 향후 연결 요청을 관리하는 데 사용되는 테이블을 overflowing하여 응답하는 기능을 공격합니다.
- 따라서 합법적인 사용자는 서버에 대한 액세스가 거부됩니다.
- 조작된 주소의 시스템이 너무 바쁘거나 존재하지 않으면 ACK가 오지 않아서 서버는 계속 SYN-ACK을 보내게 된다.
![TCP SYN Spoofing Attack](https://sundongkim-dev.github.io/assets/img/synSpoofingAttack.jpg)

## Flooding attacks
- 사용된 네트워크 프로토콜에 따라 분류됨
- 서버에 대한 일부 링크에 네트워크 용량을 오버로드하는 의도
- 사실상 모든 유형의 네트워크 패킷을 사용할 수 있습니다.

1. ICMP flood
  - ICMP echo request 패킷을 사용한 ping floods
  - 전통적으로 ping은 유용한 네트워크 진단 도구이기 때문에 네트워크 관리자는 이러한 패킷을 네트워크에 허용한다.

2. UDP flood
  - 대상 시스템의 일부 포트 번호로 향하는 UDP 패킷을 사용합니다.

3. TCP SYN flood
  - TCP 패킷을 대상 시스템으로 보냅니다.

## Distributed Denial of Service (DDoS) Attacks
여러 시스템을 사용하여 공격을 발생하며 공격자는 운영 체제 또는 일반 응용 프로그램의 결함을 사용하여 액세스 권한을 얻고 해당 프로그램에 프로그램(좀비)을 설치합니다. 하나의 공격자의 통제 하에 있는 위와 같은 시스템의 대규모 집합은 봇넷을 형성하면서 생성될 수 있다.  

**DDos Attack Architecture**
Attacker - Handler Zombies - Agent Zombies - Target

## Session Initiation Protocol (SIP) Flood
- VoIP 표준 프로토콜
- HTTP와 유사한 구문을 가진 텍스트 기반 프로토콜
- 두 가지 유형의 SIP 메시지: requests 및 responses
- 공격
  - 스푸핑된 IP 주소를 가진 수많은 INVITE requests들로 SIP proxy를 flood시킬 수 있음
![SIP Flood](https://sundongkim-dev.github.io/assets/img/SIPflood.jpg)

## Hypertext Transfer Protocol (HTTP) Based Attacks
1. HTTP flood
  - HTTP 요청으로 웹 서버를 공격하는 공격
  - 상당한 자원을 소비함
  - Spidering
    - 지정된 HTTP 링크에서 시작하여 제공된 웹 사이트의 모든 링크를 재귀적인 방식으로 따르는 봇
2. Slowloris
- 절대 완료되지 않는 HTTP 요청을 전송하여 독점하려는 시도
- 결국 웹 서버의 연결 용량을 소모함
- 합법적인 HTTP 트래픽을 활용합니다.
- 서명을 사용하여 공격을 탐지하는 기존 침입 탐지 및 방지 솔루션은 일반적으로 Slowloris를 인식할 수 없습니다.

## Reflection Attacks
- 공격자는 실제 대상 시스템의 스푸핑된 source address를 사용하여 중개자의 알려진 서비스로 패킷을 보냅니다.
- 매개자가 응답하면 응답이 대상으로 전송됩니다.
- 중개인으로부터 공격(응답)을 반사한다.
- Goal은 대상 시스템에 대한 링크를 중개자에게 알리지 않고 플러딩할 수 있는 충분한 패킷 볼륨을 생성하는 것입니다.
이러한 공격에 대한 기본적인 방어는 **스푸핑된 소스 패킷을 차단**하는 것입니다.
ex) **DNS Reflection Attacks**

## Amplification Attacks
- 합법적인 DNS 서버를 향한 패킷을 중간 시스템으로 사용
- 공격자는 target 시스템의 스푸핑된 소스 주소를 포함하는 일련의 DNS 요청을 생성합니다.
- DNS 동작을 이용하여 작은 요청을 훨씬 더 큰 응답(Amplification)으로 변환
- target에는 응답이 flooding합니다.
- 이 공격에 대한 기본적인 방어는 스푸핑된 소스 주소의 사용을 방지하는 것이다.
ex) DNS Amplification Attacks

## DoS Attack Defenses
이러한 공격은 완전히 막을 수 없으며 많은 트래픽 볼륨이 합법적일 수도 있다. ex) 특정 사이트에 대한 홍보, 인기 있는 사이트의 활동...
DDoS 공격의 방어는 다음과 같다.
1. 공격 당하기 전에 attack prevention & preemption
2. 공격 중에 Attack detection & filtering
3. 공격 중과 공격 후에 공격 소스 추적 및 식별
4. 공격 후에 Attack reaction

## DoS Attack Prevention
- 스푸핑된 소스 주소 차단
  - 가능한 소스에서 가까운 라우터에서
- 필터는 claimed source address로 되돌아가는 경로가 현재 패킷에서 사용되는 경로인지 확인하는 데 사용될 수 있습니다.
  - ISP의 네트워크를 떠나기 전에 또는 트래픽의 네트워크에 대한 진입점에서 필터가 적용되어야 합니다.
- 수정된 TCP 연결 handling code 사용
  - 서버의 초기 시퀀스 번호로 전송되는 쿠키에 중요한 정보를 암호로 인코딩합니다.
    - 합법적인 클라이언트는 incremented sequence number cookie를 포함하는 ACK 패킷으로 응답합니다.
  - 불완전한 연결에 대한 항목이 오버플로될 때 TCP 연결 테이블에서 삭제

- Block IP directed broadcasts
- 의심스러운 서비스와 조합을 차단합니다.
- 그래픽 퍼즐(capcha)의 형태로 애플리케이션 공격을 관리하여 합법적인 human requests 식별
- 고성능 및 안정성이 필요한 경우 미러 및 복제 서버 사용

## Responding to DoS Attacks
**양호한 사고 대응 계획**
- ISP의 기술자에게 연락하는 방법에 대한 세부 정보
- upstream 트래픽 필터링을 적용하는 데 필요
- 그 공격에 대한 대응 방법에 대한 세부 사항

Antispoofing, directed broadcast, rate limiting filters는 모두 구현되어 있어야 하며, 네트워크 모니터와 IDS를 통해 비정상적인 트래픽 패턴을 감지하고 통지합니다.

- 공격의 유형을 파악
  - 패킷 캡처 및 분석
  - 업스트림 공격 트래픽을 차단하는 필터 설계
  - 시스템/애플리케이션 버그를 식별하고 수정
- ISP 추적 패킷(source로 돌아가는) 사용
  - 어렵고 시간이 많이 걸릴 수 있다.
  - 법적 조치를 계획하는 경우 필요
- 비상 계획 마련
  - 대체 백업 서버로 전환
  - 새 주소로 새 사이트에 새 서버를 위탁
- 사고 대응 계획 업데이트
  - 공격과 향후 대처에 대한 대응책을 강구
