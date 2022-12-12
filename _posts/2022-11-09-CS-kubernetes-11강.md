---
published: true
title: '[쿠버네티스] Chapter 8. Persistent Volumes'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

Persistent volume으로 애플리케이션 데이터 유지하는 법에 대해 알아보자

### Decoupling pods from the infrastructure
Pod manifest에서 gcePersistentDisk 볼륨을 정의하는 애플리케이션을 AWS 클라우드에 배포하려면 어떻게 해야 할까?

직접적인 IP 주소를 표기하면 클러스터에 따라 팟이 볼륨을 사용할 수 없을지도 모른다. 어떤 클러스터에선 해당 IP 주소에 network storage가 있을 수 있지만 다른 IP 주소를 갖고 있을 수도 있기 때문이다.

### Persistent Volumes and Claims
![PVC_PV2](https://sundongkim-dev.github.io/assets/img/kubernetes/PVC_PV2.png)

- PersistentVolume object: storage volume에 대한 정보
- PersistentVolumeClaim objects: 애플리케이션의 high-level 스토리지 요구사항

더 이상 pod의 volume 정의를 어떤 network storage를 바로 가리키는 것이 아니라 PVC object를 가리키게 된다. 그 PVC는 다시 PV를 가리키게 되고 PV는 사용하게 될 network storage를 가리키게 된다.

이러한 과정을 통해, 인프라에 관련 세부 내용은 애플리케이션과 분리된다. 클러스터 관리자가 인프라 관련 low-level 내용을 포함하는 PV object를 생성해야하며, 개발자는 팟과 PVC만으로 자신의 애플리케이션을 설명하는 데만 집중할 수 있게 한다.

![PVC_PV3](https://sundongkim-dev.github.io/assets/img/kubernetes/PVC_PV3.png)

![PVC_PV4](https://sundongkim-dev.github.io/assets/img/kubernetes/PVC_PV4.png)

### Lifecycle of PV, PVC, and Pods
![lifecycleOfPV](https://sundongkim-dev.github.io/assets/img/kubernetes/lifecycleOfPV.png)

만약, PVC가 삭제된다면, PV 또한 bound에서 released 상태로 바뀌며 어떤 claim에도 bound되지 않게 된다.

이 때, volume의 reclaim policy가 Delete라면, claim이 삭제됨과 동시에 PV object와 volume 모두 삭제된다.

하지만, volume의 reclaim policy가 Retain이라면, volume이 다시 사용가능할 수 있게 된다. 해당 볼륨의 파일을 유지할지 말지는 관리자가 선택할 수 있다.

### Dynamic provisioining of PVs

앞서 살펴본 PV는 관리자가 static하게 제공했어야 했다. 미리 물리적 볼륨을 구성하고 PV object를 만들어줬기 때문이다. 하지만 동적 제공 방식에서는 관리자가 persistent volume provisoner를 배포하면 알아서 제공할 수 있게 된다. 이 과정에서 관리자는 storage class들을 설정하게 된다. 사용자는 어떤 storage가 지원되는 지 알 수 있게 되고 지원이 가능한 storage에 대해 PVC를 생성한다. 이후 provisoner가 PV를 만들어서 제공하고 K8s가 PV와 PVC를 바인드해서 volume이 마운트된다.

![dynamicProvisioning](https://sundongkim-dev.github.io/assets/img/kubernetes/dynamicProvisioning.png)

StorageClass 개체는 동적으로 프로비저닝할 수 있는 스토리지 클래스를 나타냅니다.

각 StorageClass는 어떤 provisoner를 사용할 지와 매개 변수들을 지정한다. 사용자는 그저 PVC에 사용할 스토리지 클래스를 결정하기만 하면 된다.

![storageClass](https://sundongkim-dev.github.io/assets/img/kubernetes/storageClass.png)

만약, storageClassName 필드가 standard이거나 생략되어있다면 default storage class가 사용되게 된다.

`Dynamically provisioned volume의 생명주기`  
![dynamicProvisioning2](https://sundongkim-dev.github.io/assets/img/kubernetes/dynamicProvisioning2.png)
