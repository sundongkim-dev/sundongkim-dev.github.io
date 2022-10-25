---
published: true
title: '[쿠버네티스] Chapter 4. Introducing the Kubernetes API objects'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

들어가기 앞서서, Kubernetes Design principles를 배워보기로 하자.

### Kubernetes Design principles: Understand Why

#### Kubernetes
- 컨테이너화가 핵심이었다.
  - 다양한 시스템에서 일관되고 반복 가능하며 안정적인 구현
- 누가 그것을 관리할 것인가?
  - 쿠버네티스가 클러스터를 관리
    - 컨테이너형 워크로드 배포 및 모니터링

#### How to deploy a workload?

사용자가 모든 컨테이너/노드의 상태 모니터링 및 저장하고 호출을 놓친 모든 실패한 노드를 "catch up"해야 한다. 예를 들어, 컨테이너가 crash되고 죽는다면? 노드가 crash되고 죽는다면? 이는 복잡하고 custom logic이 필요하기에 좋은 답이 아니다.

### Principle #1. Kubernetes APIs are declarative rather than imperative.

#### Declarative APIs

이전에는 사용자가 원하는 상태로 운영하기 위한 정확한 지침을 제공하고 시스템은 그 명령을 실행했다. 또한 사용자가 시스템을 모니터링하고 시스템이 이탈할 경우 추가 지침을 제공했다.

이젠, **사용자가 원하는 상태를 정의**하면 시스템이 알아서 그 상태로 다다르게 된다.

즉, 사용자가 삭제할 때까지 kube API 서버에 유지되는 API object를 만들고 시스템은 모든 컴포넌트들이 병렬로 작동하여 해당 상태로 구동된다.

왜 imperative하지 않고 declarative하게 했는가? 바로 automatic recovery 때문이다. Node에 failure가 발생하면 시스템은 pod을 healthy node로 옮겨준다.

노드는 무엇을 해야할지 어떻게 알 수 있을까?

방법 중 하나로 Master node가 worker node에게 직접 시키는 방법이다. 그러면 Master node는 앞선 사용자처럼 모니터하고 상태를 저장해야 하는데 그러면 master는 너무 복잡해진다.

### Principle #2. The Kubernetes control plane is transparent. There are no hidden internal APIs.

앞선 방법으론 마스터가 노드를 원하는 상태로 구동하기 위한 정확한 지침 세트를 제공하고 노드가 명령을 실행한다. 마스터는 이를 모니터링하고 상태가 변경될 경우 추가 지침을 제공한다

이젠, 마스터가 원하는 노드 상태를 정의합니다. 그러면 노드가 독립적으로 작동하여 해당 상태로 다다른다.

#### No Hidden Internal APIs

모든 컴포넌트는 Kubernetes API를 보고 무엇을 해야 하는지 파악한다. 예를 들면, 마스터 스케쥴러가 API server에 있는 pod A definition을 읽고 노드 B에 pod a를 생성하라고 했으니 그렇게 결정해준다.

Declarative API는 컴포넌트에 동일한 이점을 제공한다. 에지 트리거 대신 컴포넌트 레벨 트리거로 "missing events" 문제가 없다.
또한, 구성 요소의 장애로부터 쉽게 복구할 수 있고 보다 단순하고 강력한 시스템을 구축할 수 있다.
- single point of failure 없음
- 단순한 마스터 컴포넌트

Kubernetes API는 워크로드에 많은 데이터를 가지고 있다.
- 비밀: KubeAPI에 저장된 중요한 정보
  - 암호, 인증서 등
- ConfigMap – KubeAPI에 저장된 구성 정보
  - 응용 프로그램 시작 매개 변수 등
- DownwardAPI – KubeAPI의 포드 정보
  - 현재 포드의 이름 / 네임스페이스 / uid

Kube API 데이터를 가져올 때 응용 프로그램은 비밀, 구성 맵 등의 정보를 어떻게 가져오는가?
  - 원칙: 숨겨진 내부 API 없음
  - 생각할만한 솔루션: API 서버에서 직접 읽도록 앱을 수정

### Principle #3. Meet the user where they are.

쿠버네티스를 인식하도록 앱을 수정할 수도 있지만 만약 앱이 파일이나 환경 변수에서 config나 비밀 데이터를 로드할 수 있다면 수정할 필요가 없다.
![p3](https://sundongkim-dev.github.io/assets/img/kubernetes/principle3.png)
Kubernetes에서 워크로드를 구현하기 위한 장애물을 최소화한다.

#### Remote storage
포드 정의에서 원격 볼륨(GCE PD, AWS EBS, NFS 등)을 직접 참조할 수 있고 Kubernetes는 자동으로 워크로드에 사용할 수 있도록 한다.
![remote_storage](https://sundongkim-dev.github.io/assets/img/kubernetes/remote_storage.png)

### Principle #4. Workload portability

**PVC/PV**  
Persistent Volume 및 Persistent Volume Claim 추상화: 스토리지 구현과 스토리지 사용량 분리
![PVC_PV](https://sundongkim-dev.github.io/assets/img/kubernetes/PVC_PV.png)

쿠버네티스가 OS처럼 추상화 레이어 역할을 하게 된다.

---
### Introducing the Kubernetes API Obejcts
![kubernetes API](https://sundongkim-dev.github.io/assets/img/kubernetes/kubernetes_API.png)

Kubernetes API는 POST, GET, PUT/Patch 또는 DELETE와 같은 표준 HTTP 메서드를 사용하여 CRUD 작업(생성, 읽기, 업데이트, 삭제)을 수행하는, 리소스로 상태를 나타내는 HTTP 기반 RESTful API입니다. 클러스터의 구성을 나타내는 것은 이러한 리소스(또는 개체)입니다.

**Resource vs. Object**  
RESTful API의 기본 개념은 리소스이며, 각 리소스에는 고유하게 식별되는 URI 또는 Uniform Resource Identifier가 할당된다. 예를 들어, Kubernetes API에서 애플리케이션 배포는 배포 리소스로 표시된다. 클러스터의 모든 배포 컬렉션은 /api/v1/deployment에 노출된 REST 리소스이다. GET 방법을 사용하여 이 URI로 HTTP 요청을 보내면 클러스터의 모든 배포 인스턴스를 나열하는 응답을 수신한다.

![Resource object](https://sundongkim-dev.github.io/assets/img/kubernetes/resource_object.png)

또한 각 개별 배포 인스턴스에는 조작할 수 있는 고유한 URI가 있어서 개별 deployment는 또 다른 REST 자원으로 노출된다. GET 요청을 리소스 URI로 전송하여 배포에 대한 정보를 검색할 수 있으며 PUT 요청을 사용하여 수정할 수 있다.

Object는 둘 이상의 리소스를 통해 노출될 수 있다. 리소스가 object를 전혀 나타내지 않는 경우도 있다. 이것의 예는 Kubernetes API가 클라이언트가 주체(사람 또는 서비스)가 API 연산을 수행할 권한이 있는지 여부를 확인할 수 있도록 하는 방법이다. 이 작업은 POST 요청을 /syslog/authorization.k8s.io/v1/subjectaccessreviews 리소스에 제출하여 수행된다. 응답은 환자가 요청 본문에 지정된 작업을 수행할 수 있는 권한이 있는지 여부를 나타냅니다. 여기서 중요한 것은 POST 요청에 의해 object가 생성되지 않는다는 것입니다.

### Object Manifest
대부분의 쿠버네티스 API 객체의 매니페스트는 다음과 같은 4개의 섹션으로 구성된다.
- Type metadata: Object type, group, api version
- Object metadata: Object instance의 기본적인 정보(object 이름, 생성 시간, 소유자 등)
- Spec: Object의 desired state
- Status: Object의 현재 상태

### Managing an Object
Object의 가장 중요한 두 부분은 사양 및 상태 섹션이다. Spec을 사용하여 원하는 개체 상태를 지정하고 Status 섹션에서 개체의 실제 상태를 읽을 수 있습니다. 그럼, 스펙을 작성하고 상태를 읽는 사람은 당신이지만, 스펙을 읽고 상태를 작성하는 것은 무엇일까..? 바로 컨트롤러이다.

![controller](https://sundongkim-dev.github.io/assets/img/kubernetes/controller.png)

Kubernetes 컨트롤 평면은 사용자가 만든 개체를 관리하는 컨트롤러라는 여러 컴포넌트를 실행한다. 각 컨트롤러는 일반적으로 하나의 개체 유형만 담당한다. 예를 들어 배포 컨트롤러는 배포 개체를 관리한다.


### Event Object

**Event Object를 통한 클러스터 이벤트 관찰**  
컨트롤러는 객체의 사양 필드에 지정된 대로 객체의 실제 상태를 원하는 상태와 조정하는 작업을 수행할 때 이벤트를 생성하여 자신이 수행한 작업을 표시한다. 일반 및 경고의 두 가지 유형의 이벤트가 있다.

Kubernetes의 다른 모든 것과 마찬가지로 이벤트는 Kubernetes API를 통해 생성되고 읽히는 Event 객체로 표현된다. Event object에는 object에 발생한 내용과 이벤트 원본에 대한 정보가 들어 있습니다.
다른 object와 달리 각 이벤트 개체는 생성 후 1시간 후에 삭제되어 쿠버네테스 API 개체의 데이터 저장소인 etcd에 대한 부담을 줄여줍니다.
![event_object](https://sundongkim-dev.github.io/assets/img/kubernetes/event_object.png)

### Kubernetes APIs
- Computing building block = Pod
- Communication building block = Service
- Grouping = Labels and Annotations
- Configuration = ConfigMap and Secrets
- Stateless pod coordination = ReplicaSet, DaemonSet, Job
- Application updates = Deployment
- Stateful pod coordination = StatefulSet
- Storage building block = PersistentVolumeClaim on top of PersistentVolume
