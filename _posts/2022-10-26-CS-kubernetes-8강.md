---
published: true
title: '[쿠버네티스] Chapter 11. Services'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

### Service
- 각 팟에는 고유한 IP 주소를 가진 고유한 네트워크 인터페이스가 있다.
- 모든 포드는 flat address space를 가진(네트워크 주소 변환 필요 X) 단일 개인 네트워크로 연결된다.

Service란 동일한 서비스를 제공하는 팟 그룹에 대한 지속적인 단일 진입 지점을 말한다. 각 서비스에는 변경되지 않는 IP 주소와 포트가 있다.
- 팟은 수명이 짧다. 즉, 일시적이다.
- Pod의 IP는 노드에 스케쥴링된 후 할당됩니다. 즉, 클라이언트는 IP를 미리 알지 못한다.
- 여러 팟이 동일한 서비스를 제공할 수 있습니다. (Horizontal scaling)
- 서비스는 포드 앞에서 로드 밸런서 역할을 한다.

![service](https://sundongkim-dev.github.io/assets/img/kubernetes/service.png)

서비스가 없다면, 키아다팟은 재시작 될때마다 quote와 quiz pod의 IP를 얻어야 한다.

![serviceDefining](https://sundongkim-dev.github.io/assets/img/kubernetes/serviceDefining.png)

- ClusterIP: Cluster IP는 클러스터 안의 Pod끼리 통신하기 위한 Private IP이다.

Service 이름을 도메인 주소로도 사용이 가능하다. 이는 바로 쿠버네티스에서 제공하는 DNS 서버가 있기 때문이다.

## Exposing services to the Outside

외부에서 서비스에 접근할 수 있도록 하기 위해 다음을 제공한다.
- ExternalIP: 추가적인 IP 할당
- NodePort: 서비스 type의 한 종류로, 각 노드는 노드 자체에서 서비스에 대한 포트를 열고 해당 포트의 트래픽을 서비스로 리디렉션한다.
- LoadBalancer: 서비스 type의 한 종류로, 클라우드 서비스 공급자의 전용 로드 밸런서를 통해 액세스 가능
- Ingress: HTTP 레벨에서 동작

### NodePort
![nodePort](https://sundongkim-dev.github.io/assets/img/kubernetes/nodePort.png)
- 클러스터의 모든 노드에 있는 특정 포트를 통해 액세스 가능
- clusterIP 서비스처럼 내부 클러스터 IP를 통해 액세스할 수 있지만 각 클러스터 노드의 노드 포트를 통해서도 액세스할 수 있다.

### LoadBalancer
![loadBalancer](https://sundongkim-dev.github.io/assets/img/kubernetes/loadBalancer2.png)
- 클라우드 인프라에서 제공하는 로드 밸런서 IP 주소를 통해 서비스에 액세스 가능
- 외부 클라이언트는 로드 밸런서의 포트 80에 연결한다.
- 노드 중 하나의 할당된 노드 포트로 라우팅된다.
- 여기서 연결은 팟 인스턴스 중 하나로 전달된다.

쿠버네티스는 각 노드의 생성 및 삭제가 자유롭다. 그때마다 노드 IP를 추적하는 일은 비효율적이다. ClusterIP 타입의 서비스가 Pod 레벨에서의 안정적인 엔드포인트를 제공하는 것이라면,  로드밸런서는 노드레벨에서의 안정적인 엔드포인트를 제공한다.

### Services endpoints
- 서비스가 팟에 직접 연결되지 않는다: 서비스 <-> 엔드포인트 <-> 포드
- Endpoint 개체에는 서비스의 endpoint를 나타내는 IP 및 포트 조합 목록이 포함되어 있다.

### EndpointSlice Object
 -엔드포인트 개체의 크기는 매우 많은 수의 엔드포인트가 있을 경우 성능 문제가 있다.
  - 변경 시 전체 개체를 모든 클러스터 노드로 전송해야 합니다.
- EndpointSlice 개체는 단일 서비스의 끝점을 여러 조각으로 분할합니다.

### Managing service endpoints

label selector가 있는 서비스 개체의 경우 쿠버네티스는 자동으로 Endpoint/EndpointSlice 개체를 만든다.

그러나 label selector가 없는 서비스의 경우에도 만들 수 있다. 이 경우 Endpoint 개체를 수동으로 관리해야 한다. 기존의 외부 서비스를 다른 이름으로 포드에 접근할 수 있게 하는 것이다.

Service/Endpoint 개체를 생성하면 팟이 다른 서비스와 동일한 방식으로 이 서비스를 사용할 수 있다. 서비스의 클러스터 IP로 전송된 트래픽은 서비스의 엔드포인트로 분산된다. 이러한 endpoint는 클러스터 외부에 있지만 내부에 있을 수도 있습니다.
![endpoint](https://sundongkim-dev.github.io/assets/img/kubernetes/endpoint.png)

### Headless services
서비스는 안정적인 IP 주소에 팟들을 노출하며, 서비스에 대한 연결은 해당 엔드포인트에 자동으로 분산된다. 하지만 클라이언트가 로드 밸런싱을 수행하도록 하거나 클라이언트가 연결할 팟을 결정해야한다면 어떻게 해야 할까?

헤드리스 서비스를 생성하여 서비스의 클러스터 IP 대신 팟 IP를 반환하도록 내부 DNS를 구성할 수 있다. 즉, 헤드리스 서비스를 통해 client는 팟에 직접 연결한다.

### Ingress object
![ingressObject](https://sundongkim-dev.github.io/assets/img/kubernetes/ingressObject.png)
- HTTP 요청의 호스트와 경로는 요청이 전달되는 서비스를 결정
- 단일 수신을 통해 여러 서비스를 노출할 수 있다.
- 애플리케이션 계층에서 작동하며 HTTP 인증, 쿠키 기반 세션 선호도, URL 다시 쓰기 등의 기능을 제공
- Ingress IP는 DNS에 추가되어야 한다.

`Path-based Ingress Traffic Routing`  
![path-based-ingress](https://sundongkim-dev.github.io/assets/img/kubernetes/path-based-ingress.png)

- pathType field
  - Exact: 입력 규칙에 지정된 경로와 정확히 일치해야 함
  - Prefix:입력 규칙에 지정된 경로로 시작해야 함

![multipleRulesIngress](https://sundongkim-dev.github.io/assets/img/kubernetes/multipleRulesIngress.png)
