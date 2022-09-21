---
published: true
title: '[분산 컴퓨팅] Chapter 2. Architectures'
layout: post
subtitle: 'csReview DistributedComputing'
categories: csReview
tags: DistributedComputing
comments: true
---

## Chapter 2: Architectures
- Architectural styles
  - Layered architectures
  - Object-based and service-oriented architectures
  - Publish-subscribe architectures
- System architecture
  - Centralized organizations
  - Decentralized organizations: peer-to-peer systems

---
### Architectural sytles

Software architecture: 다양한 소프트웨어 구성 요소의 구성 방법 및 상호 작용 방법으로 다음 3 가지 유형이 있다.
1. Centralized architectures
2. Decentralized architectures
3. Hybrid architectures

System architecture: 위의 소프트웨어 아키텍처가 최종적으로 인스턴스화(실체화)된 것을 말한다.

Architectural styles는 다음과 같이 정의될 수 있다.
- 잘 정의된 인터페이스를 가진(교체 가능한) component
- Component가 서로 연결되는 방식
- Component간에 교환되는 데이터
- Component와 **connector**가 어떻게 시스템으로서 구성되는 가?
  - Connector: Component간의 communication, coordination, cooperation을 중재하는 메커니즘으로 RPC, messaging, streaming을 위한 기능으로 예를 들 수 있다.

분산 시스템을 위한 중요한 아키텍처 스타일로는 다음의 4 가지 유형이 있다.
- Layered architectures
- Object-based architectures
- Resource-centered architectures
- Event-based architectures

#### Layered architecture
