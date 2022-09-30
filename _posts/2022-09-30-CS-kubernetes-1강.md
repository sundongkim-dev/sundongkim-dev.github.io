---
published: true
title: '[쿠버네티스] Chapter 1. Introduction'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

### Cloud Native Computing(from Wikipedia)
클라우드 네이티브 컴퓨팅(Cloud Native Computing)은 클라우드 컴퓨팅을 활용하여 public, private, hybrid clouds와 같은 현대적이고 동적인 환경에서 확장 가능한 애플리케이션을 구축하고 실행하는 소프트웨어 개발의 접근 방식이다.

Declarative code를 통해 배포된 container, microservices, serverless functions, immutable infrastructure와 같은 기술은 이러한 아키텍처 스타일의 공통 요소이다.

이러한 기술은 resilent, manageable, observable하며 loosely coupled system을 가능하게 한다. 강력한 자동화 기능을 통해 엔지니어는 최소의 노력으로 높은 영향을 미치는 변경사항을 빈번하고 예측 가능한 방식으로 변경할 수 있다.

클라우드 네이티브 애플리케이션은 도커 컨테이너에서 실행되는 일련의 마이크로 서비스로 구축되며, 쿠버네티스에서 조정되고 DevOps 및 GitCI 워크플로우를 사용하여 관리 및 배포될 수 있다.

도커 컨테이너의 장점은 실행에 필요한 모든 소프트웨어를 하나의 실행 가능한 패키지로 패키징할 수 있다는 것이다. 컨테이너는 가상화된 환경에서 실행되므로 포함된 애플리케이션을 해당 환경에서 격리한다.

- Cloud native
  + Microservices: RESTful API나 AMQ를 사용하여 application간의 통신, 독립적인 배포, 업데이트, 확장 및 재시작 지원
  + DevOps: 자동화된 릴리즈 파이프라인 및 CI 도구, 운영 환경에 신속하게 배포, 개발과 O&M의 협업
  + Continuous delivery: 잦은 release, quick delivery, 빠른 피드백 및 release 위험 감소
  + Containers: 최적의 마이크로서비스 운영

### Container
![container](https://sundongkim-dev.github.io/assets/img/kubernetes/container.png)
- 별도의 OS 없이 호스트 OS에서 프로세스가 분리되어 실행
- 개별 microservice를 위한 격리된 환경
- VM에 대한 훨씬 가벼운 대체품 – 사실상 오버헤드 없음

### Microservices Architecture(MSA)
![microservices](https://sundongkim-dev.github.io/assets/img/kubernetes/microservices.png)  
처음엔 Pre-SOA라고도 하는 monolithic하게 디자인 되었었다. 굉장히 깊게 엮여서 분리하기가 어려웠다. 2000년대에 와서 SOA로 디자인하게 되었고 좀 덜 엮인 모습을 한다.

2010년대에는 잘게 나누어져서 교체하고 업데이트하기 편해졌다. 이를 MSA라고 하고 단일 응용 프로그램을 작은 서비스들의 모음으로 개발하는 접근법이다.

**Microservices**: 하나의 책임을 다루는 소규모 논리 중심 서비스
애플리케이션을 마이크로 서비스로 분할한다. 각 마이크로서비스는 독립적인 프로세스로 실행되며 단순하고 잘 정의된 인터페이스를 통해 다른 마이크로 서비스와 통신한다.  
![microservices_2](https://sundongkim-dev.github.io/assets/img/kubernetes/microservices_2)  
Monolithic의 경우 전체 단위 자체를 복사해야하고 microservices의 경우 필요한 microservice만 늘리면 된다.

**Scaling Microservices**
위에서 처럼 scaling에 장점이 있다. Scaling에도 여러 유형이 있다.
- Scaling out vs. Scaling up
  - Scaling Out: 머신 개수 늘리기
  - Scaling In: 머신 개수 줄이기
  - Scaling Up: 리소스 할당 늘리기
  - Scaling Down: 리소스 할당 줄이기
- Horizontal scaling: 머신 개수 늘리기
- Vertical Scaling: 인스턴스에 할당된 자원 늘리기

### DevOps, MSA, and CI/CD
- DevOps = Development + Operations
- MSA = Microservices Architecture
- CI/CD = Continuous Integration / Continuous Delivery(패치 만들고 배포)
- CI/CD 파이프라인은 앱 개발 단계에 자동화를 도입해 고객에게 앱을 자주 전달하는 방식이다.
- 개발자, QA 및 운영 팀이 전체 프로세스에서 협업

### Kubernetes
조타수에 비유할 수 있다. 마치 조타수처럼 쿠버네티스는 어플리케이션을 조종하고 선장(user)에게 상태를 보고한다.

**오픈소스 컨테이너 오케스트레이션 시스템**  
- 원래 Google에서 설계했으며, 현재는 CNCF에서 관리되고 있습니다.
- 호스트 클러스터 간에 애플리케이션 컨테이너의 배포, 확장 및 운영을 자동화하는 플랫폼 제공
- KubeCon + CloudNativeCon 북미/유럽/중국

**Kubernetes in a Nutshell**
- 복잡한 대규모 애플리케이션 시스템의 배포 및 관리를 자동화하는 소프트웨어 시스템
- 기본 하드웨어에 대한 abstraction layer: 컴퓨터에게 뭘 할 필요가 없음
- 개발자가 App을 쿠버네티스를 통해 배포하면 여러 worker node들이 마치 하나의 deployment platform으로 보인다.

### Declarative Model
- Application은 declarative model에 의해 정의된다. 설명의 변경 사항은 실행 중인 응용 프로그램에 반영된다.
- Application 설계에 대한 설명 제공
- Kubernetes는 설명을 실행 중인 components 집합으로 바꿉니다.
- Kubernetes는 장애가 발생한 컴포넌트를 다시 시작하고 사라지는 컴포넌트를 다시 생성함으로써 컴포넌트가 계속 작동하도록 보장한다.

### Why Kubernetes?
- 속도
- Scaling(software & teams)
- Abstract infrastructure 제공
- 효율성(resource utilization)

### Operating System for Computer Clusters
- Kubernetes는 플랫폼을 구축하기 위한 플랫폼이다.
- 분산 애플리케이션과 클러스터 간의 인터페이스(OS 역할)
  - Service discovery, horizontal scaling, load-balancing(request 골고루 분산)
  - 서비스 검색, 수평 확장, 로드 밸런싱, 자가 복구, 리더 선출 등
- 앱 개발자는 핵심 비즈니스 로직을 구현하는 데 집중할 수 있다

**Kubernetes Cluster**
