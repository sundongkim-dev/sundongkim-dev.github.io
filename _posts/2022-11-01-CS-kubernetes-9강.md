---
published: true
title: '[쿠버네티스] Chapter 12. Deployments'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

## ReplicaSet
ReplicaSet은 팟 복제본들의 그룹을 말한다. 팟을 하나씩 작성하는 대신 pod template과 replica count만으로 replicaSet object를 생성할 수 있다.

![replicaSet](https://sundongkim-dev.github.io/assets/img/kubernetes/replicaSet.png)

- 노드에 장애가 발생한 경우 팟을 복제하고 다시 스케쥴링하는데 사용된다
- Label selector: 어떤 팟을 복제할 것인가
- Replica count: 원하는 복제 팟의 수
- Pod template: 새 팟 복제본을 생성할때 사용
- 일반적으로 higher-level 배포 리소스를 생성할 때 자동으로 생성된다

결국, replicaSet이 갖고 있는 pod들을 관리한다.

![replicaSet2](https://sundongkim-dev.github.io/assets/img/kubernetes/replicaSet2.png)

템플릿에서 팟 이름이 지정되지 않고 ReplicaSet 이름에서 생성된다. 또한 pod template(manifest)을 수정하여 생성되는 팟을 변경할 수 있다.

ReplicaSet과 그의 팟들을 다 지울수도 있고 오직 replicaSet만 지워서 팟은 남길 수도 있다.

---
## Deployment
![deployment](https://sundongkim-dev.github.io/assets/img/kubernetes/deployment.png)
ReplicaSets 맨 위에 있는 상위 수준의 리소스 개체로 deployment 개체는 ReplicaSet 개체를 통해 포드 개체를 관리한다. 애플리케이션을 배포하고 선언적으로 업데이트하기 위한 용도이며 ReplicaSets와 마찬가지로 배포에서 팟 템플릿, replica count, label selector를 지정해준다. 또한 업데이트 전략도 지정된다.

### Label Selectors in Deploy, RS, and PO
RepicaSet 및 Pod 레이블 모두에 있는 추가적으로 pod-template-hash 레이블이 있다. 이는 replica의 selector field에도 나타난다. 팟 템플릿 해시 레이블은 포드 템플릿의 내용으로 산출되므로 팟 템플릿을 변경할 때마다 새로운 replicaSet이 만들어진다.

![podTemplateHash](https://sundongkim-dev.github.io/assets/img/kubernetes/podTemplateHash.png)

만약, deployment를 scaling하면 어떻게 될까? Deployment controller는 replicaSet의 replica count를 변경하고 replicaSet의 replica count를 변경되면 replicaSet controller이 알아서 팟을 더 생성하게 되는 것이다.

### Two Update strategies
배포에서 팟 템플릿을 업데이트하면 포드가 교체된다. 앞서 본 ReplicaSet의 경우 교체되지 않고 새 포드를 만들 때만 사용하게 된다.

![deploymentStrategies](https://sundongkim-dev.github.io/assets/img/kubernetes/deploymentStrategies.png)

1. Recreate
  - 포드 이름은 ReplicaSet에서 가져오므로 이름이 바뀌었다면 다른 ReplicaSet에 속함을 나타낸다.
![recreate](https://sundongkim-dev.github.io/assets/img/kubernetes/recreate.png)

2. RollingUpdate (default 전략)
  - 포드를 점진적으로 대체하는 기본 전략으로 이전 replicaSet이 축소됨과 동시에 새로운 replicaSet이 생성되고 scaling up된다.
  - rollout되는 과정을 확인할 수 있고, 그 과정을 롤백할수도, 일시정지할수도 재개할수도 있다.
  -
![rollingUpdate](https://sundongkim-dev.github.io/assets/img/kubernetes/rollingUpdate.png)

3. Canary
  - 하나 또는 매우 적은 수의 새 팟을 만들고 소량의 트래픽을 해당 팟으로 리디렉션하여 예상대로 작동하는지 확인하고 괜찮으면 나머지 포드를 모두 교체한다.
![canary](https://sundongkim-dev.github.io/assets/img/kubernetes/canary.png)

4. A/B testing
  - 소수의 새 팟을 만들고 일부 사용자를 특정 조건에 따라 해당 팟으로 리디렉션한다. 단일 사용자는 항상 동일한 버전의 응용프로그램으로 리디렉션된다. 일반적으로 이 전략을 사용하여 각 버전이 특정 목표를 달성하는 데 얼마나 효과적인지에 대한 데이터를 수집한다.
  ![ABtesting](https://sundongkim-dev.github.io/assets/img/kubernetes/ABtesting.png)

4. Blue/Green
  - 새 버전의 팟을 이전 버전과 병렬로 배포한다. 새 팟이 준비될 때까지 기다린 다음 모든 트래픽을 새 포드로 전환한다.
  ![BG](https://sundongkim-dev.github.io/assets/img/kubernetes/BG.png)

5. Traffic Shadowing
  - 새 버전의 팟을 이전 버전과 함께 배포하여 각 요청을 두 버전 모두로 전달하지만 새 버전의 응답은 무시하고 이전 버전의 응답만 사용자에게 반환한다. 이렇게 하면 새 버전이 사용자에게 영향을 미치지 않고 작동하는 방식을 확인할 수 있다.
  ![shadowing](https://sundongkim-dev.github.io/assets/img/kubernetes/shadowing.png)
---
