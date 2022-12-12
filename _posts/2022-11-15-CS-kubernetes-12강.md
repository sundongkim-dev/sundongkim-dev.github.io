---
published: true
title: '[쿠버네티스] Chapter 13. StatefulSets'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

StatefulSets을 이용해서 stateful한 어플리케이션을 배포하는 것에 대해 알아보자

### Replicating Stateful Pods
ReplicaSets는 이름과 IP 주소를 제외하고 서로 같은 여러 팟 인스턴스를 만들게 된다. 즉, 모든 replica들이 같은 팟 템플릿으로부터 만들어지기 때문에 같은 PVC와 PV를 갖게 된다.

![replicaSetPVC](https://sundongkim-dev.github.io/assets/img/kubernetes/replicaSetPVC.png)

replica들에 각기 다른 스토리지를 부여하려면 어떻게 해야할까?
1. 팟들을 수동적으로 생성
2. 하나의 팟 인스턴스에 하나의 replicaSet 사용
![dedicatedPVC](https://sundongkim-dev.github.io/assets/img/kubernetes/dedicatedPVC.png)
3. 같은 볼륨에서 여러 디렉터리 사용  
![multipleDirectories](https://sundongkim-dev.github.io/assets/img/kubernetes/multipleDirectories.png)

### StatefulSets vs. ReplicaSets

Stateful app들에서 앱 인스턴스는 애완동물로 비유할 수 있지만 stateless app들에서는 소들에 비유할 수 있다.

ReplicaSets의 pod replica들은 소들에 비유할 수 있는데, 이는 곧 언제나 새로운 pod replica로 교체될 수 있기 때문이다.

반면, StatefulSet은 그렇지 않다. 각각의 인스턴스가 stable name과 state를 갖고 non-fungible하게 취급된다. 팟이 자신의 identity와 state를 유지하도록 하며 replicaSet에서 만든 팟과 달리 서로의 정확한 replica가 아니다.

### Stable Network Identity
StatefulSet에 의해 생성된 각 팟에는 순서형 인덱스가 할당된다. 팟의 이름과 호스트 이름을 도출하고 팟에 안정적인 스토리지를 부착하는 데 사용된다.
![stableNetworkIdentity](https://sundongkim-dev.github.io/assets/img/kubernetes/stableNetworkIdentity.png)

Stateful pod은 hostname으로 주소를 지정할 수 있어야 한다. Governing headless service 각 팟에 네트워크 ID를 제공하기 위해 생성됩니다. 교체 팟은 사라진 팟과 동일한 이름과 hostname을 얻는다.

Scaling할 때에도 역시 인덱스 순서대로 커졌다가 줄어들었다가하게 된다. 즉 지울 때 제일 큰 인덱스부터 지워진다.

### Dedicated Storage
각 Stateful pod 인스턴스는 자체 스토리지를 사용해야 합니다. 스토리지는 영구적이어야 하며 팟과 분리되어야 한다. StatefulSet에는 volume claim template이 있어서 PVC와 팟 인스턴스를 분리할 수 있다.

![dedicatedStorage](https://sundongkim-dev.github.io/assets/img/kubernetes/dedicatedStorage.png)

Scaling down하면 팟만 삭제되고 claim은 그대로 유지(PVC 유지)된다. Scale up할 때 재사용할 수 있게 된다. 결과적으로, 기본 PV를 해제하려면 PVC를 수동적으로 삭제해야 한다.

![dedicatedStorage2](https://sundongkim-dev.github.io/assets/img/kubernetes/dedicatedStorage.png)

### Using a StatefulSet
애플리케이션을 배포하려면 다음을 생성해야 한다.
- 데이터 파일들을 저장하기 위한 PersistentVolumes (Dynamic provisioining of PVs 지원안할 경우)
- StatefulSet을 위한 governing service
- StatefulSet

각 팟에 대해서 StatefulSet은 PV에 바인딩되는 PVC를 생성한다.

Governing service는 각 팟이 DNS entry를 갖게 한다. 따라서 팟 간의 peer discovery가 가능해진다.

VolumeClaimTemplates은 data(각 팟에 대한 PVC를 생성하는 데 사용)라는 하나의 볼륨 클레임 템플릿을 정의한다.
- Stateless pod의 경우 PersistentVolumeClaim volume이 manifest에 포함된다
- Stateful pod의 경우 자동적으로 수행된다. 볼륨이 클레임(특정 팟에 대해 생성된 statefulSet claim)에 바인딩 된다.

생성된 PVC의 이름은 volumeClaim에 정의된 이름과 팟의 이름으로 구성된다.

Stateful pod들을 노출시킬수도 있지만 클라이언트는 일반적으로 직접 연결하기보다 서비스를 통해 팟을 연결한다. 
