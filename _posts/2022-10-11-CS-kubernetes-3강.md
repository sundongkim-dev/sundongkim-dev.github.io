---
published: true
title: '[쿠버네티스] Chapter 3. Deploying your first application'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

### Deploying a Kubernetes Cluster
- 랩톱, 조직의 인프라 또는 클라우드 프로바이더의 VM
- Local kubernetes cluster
  - MacOS 또는 Windows의 도커 데스크톱
  - Minikube
  - Kind(Kubernetes-in-Docker)
  - Kubeadm

- Managed Kubernetes services
  - 구글 쿠버네티스 엔진(GKE)
  - 아마존 엘라스틱 쿠버네티스 서비스(EKS)
  - 마이크로소프트 AKS(Azure Kubernetes 서비스)
  - IBM 클라우드 쿠버네티스 서비스
  - 알리바바 클라우드 컨테이너 서비스

### Using Minikube
![minikube](https://sundongkim-dev.github.io/assets/img/kubernetes/minikube.png)

### Interacting with Kubernetes
![kubectl](https://sundongkim-dev.github.io/assets/img/kubernetes/kubectl.png)

---
### Pods
Kubernetes에서는 개별 컨테이너를 배포하는 대신 같은 위치에 배치된 컨테이너 그룹(pod)을 배포합니다.

팟(pod)은 동일한 작업자 노드에서 함께 실행되며 특정 리눅스 네임스페이스를 공유해야 하는 하나 이상의 밀접하게 관련된 컨테이너의 그룹이다. 포드 사양에 따라 동일한 네트워크와 UTS 네임스페이스를 사용한다.

각 포드는 하나의 애플리케이션을 포함하는 별도의 논리적 컴퓨터라고 생각할 수 있다. 애플리케이션은 컨테이너에서 실행되는 단일 프로세스 또는 별도의 컨테이너에서 실행되는 주요 애플리케이션 프로세스와 추가 지원 프로세스로 구성될 수 있다. 포드는 클러스터의 모든 worker 노드에 분산된다.

각 포드에는 자체 IP, 호스트 이름, 프로세스, 네트워크 인터페이스 및 기타 리소스가 있다. 동일한 포드의 일부인 컨테이너는 컴퓨터에서 실행되는 유일한 컨테이너라고 생각한다. 또한, 같은 노드에 위치하더라도 다른 포드의 프로세스를 볼 수 없다.
![pods](https://sundongkim-dev.github.io/assets/img/kubernetes/pods.png)

![behind the scenes](https://sundongkim-dev.github.io/assets/img/kubernetes/kubectl_process.png)

각 포드는 자체 IP 주소를 얻지만 이 주소는 클러스터 내부이며 외부에서 액세스할 수 없다. 외부에서 포드에 액세스할 수 있도록 하려면 서비스 object를 생성해야 한다. 여러 서비스 object가 있는데, 일부는 클러스터 내에서만 포드를 노출하는 반면, 다른 일부는 포드를 외부로 노출합니다. loadBalancer 유형의 서비스는 외부 로드 밸런서를 프로비저닝하여 공용 IP를 통해 서비스에 액세스할 수 있도록 합니다.

### Exposing your app to the world
Kubernetes는 이른바 LoadBalancer 서비스를 만들 수 있지만 로드 밸런서 자체를 제공하지는 않는다. 클러스터가 클라우드에 배포된 경우 Kubernetes는 클라우드 인프라에 로드 밸런서를 프로비저닝하도록 요청하고 트래픽을 클러스터로 전달하도록 구성할 수 있다. 인프라에서 Kubernetes에게 로드 밸런서의 IP 주소를 알려주면 이 주소가 서비스의 외부 주소가 됩니다.

![loadBalancer](https://sundongkim-dev.github.io/assets/img/kubernetes/loadBalancer.png)

일부 Kubernetes 클러스터에는 로드 밸런서를 제공하는 메커니즘이 없다. 미니큐브가 제공하는 클러스터도 그중 하나다.

### Horizontally scaling the application
컨테이너에서 애플리케이션을 실행하는 주요 이점 중 하나는 애플리케이션 배포를 쉽게 확장할 수 있다는 것이다.

애플리케이션을 사용하는 사용자가 갑자기 더 많아지면 단일 인스턴스는 더 이상 로드를 처리할 수 없게 된다. 부하를 분산하고 사용자에게 서비스를 제공하려면 추가 인스턴스를 실행해야 하는데 이를 scale-out이라고 한다.

![horizontally_scaling](https://sundongkim-dev.github.io/assets/img/kubernetes/horizontally_scaling.png)

Kubernetes 서비스 자체에서 제공되며, GKE 또는 클라우드에서 실행되는 다른 클러스터가 실행될 때 인프라에서 제공하는 추가 로드 밸런서가 제공됩니다.

Minikube를 사용하고 외부 로드 밸런서가 없는 경우에도 요청은 서비스 자체에 의해 세 개의 포드로 분산됩니다. GKE를 사용하면 실제로 두 개의 로드 밸런서가 작동한다.

위 그림에서는 인프라에서 제공하는 로드 밸런서가 요청을 노드 전체에 분산한 다음, 서비스가 포드 전체에 요청을 분산하는 것을 보여 줍니다.
---
### API Object view of the app
시스템을 바라보는 방법에는 논리적 보기와 물리적 보기라는 두 가지가 있는데 위의 그림에서 물리적 뷰를 보았다. 세 개의 worker 노드(Minikube를 사용하는 경우 단일 노드)에 배포되는 세 개의 실행 중인 컨테이너가 있다. 클라우드에서 Kubernetes를 실행하면 클라우드 인프라에서 로드 밸런서도 생성된다. 미니큐브는 로드 밸런서를 생성하지 않지만 노드 포트를 통해 서비스에 직접 액세스할 수 있습니다.

클러스터마다 시스템의 물리적 뷰에 차이가 있지만, 논리적 뷰는 항상 동일하다.  
![object_view](https://sundongkim-dev.github.io/assets/img/kubernetes/obejct_view.png)
Obejct는 다음과 같습니다.
- 생성한 배포 Obejct,
- 배포에 따라 자동으로 생성된 포드 Obejct 및 수동으로 생성한 서비스 Obejct
