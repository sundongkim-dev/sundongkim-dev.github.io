---
published: true
title: '[쿠버네티스] Chapter 7. Storage Volumes'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

팟의 컨테이너에 Storage volume을 마운팅하는 것에 대해 알아보자.

### Persisting Files across Container Restarts
컨테이너의 파일 시스템에 있는 파일은 빌드 시간 동안 컨테이너 이미지에 추가된 파일이다.

즉, 종료하고 다시 시작하면 파일에 대한 모든 변경 내용이 사라지는데 재시작함에도 변경 내용들을 유지하려면 어떻게 해야 할까..?

팟에 볼륨을 추가하고 컨테이너에 마운트하자!!

### Volume
볼륨은 팟 레벨에서 정의된다. 그 후, 컨테이너에 원하는 위치에 마운트한다. 결국, 볼륨은 팟의 생명주기에 묶이게 된다. (컨테이너의 생명주기가 아니다!)

결과적으로, 컨테이너가 재시작해도 데이터를 유지할 수 있게 된다.
![volume](https://sundongkim-dev.github.io/assets/img/kubernetes/volume.png)
![volume2](https://sundongkim-dev.github.io/assets/img/kubernetes/volume2.png)

- 하나의 팟은 여러 개의 volume들을 가질 수 있다
- 각 볼륨들은 컨테이너의 분리된 곳에 마운트된다
- 컨테이너는 팟의 모든 볼륨을 마운트할 필요 없이 필요한 것만 마운트하면 된다
- 하나의 볼륨이 여러 컨테이너에 마운트될 수도 있다.
  - 이 때, 볼륨의 mode는 read-write / read-only 등으로 설정 가능
  - 각 컨테이너에서 각기 다른 mount path 설정 가능

볼륨은 팟의 생명주기에 묶여서 팟이 살아있을 때에만 존재한다고 했지만 pod 밖에다가 매핑할수도 있다. ex) NAS volume
![persistingData](https://sundongkim-dev.github.io/assets/img/kubernetes/persistingData.png)
![sharingData](https://sundongkim-dev.github.io/assets/img/kubernetes/sharingDatan.png)

### Volume types
- emptyDir: 팟이 시작되기 직전에 생성되고 처음에는 비어 있는 단순 디렉터리
  - 포드가 존재하는 동안 보존됨
- hostPath: 작업자 노드의 파일 시스템에서 팟으로 파일을 마운트하는 데 사용
  - Kubernetes는 기본 인프라를 추상화해야하지만 노드의 파일 시스템에 액세스해야 하는 system-level 팟인 경우 예외에 해당된다.
  - hostPath 볼륨이 호스트 노드의 파일 시스템에서 특정 위치를 가리킨다.
  - hostPath 볼륨에 동일한 경로가 있으면 동일한 노드의 팟은 동일한 파일에 액세스하지만 다른 노드의 포드는 액세스하지 않는다. 즉, 각각 다른 파일에 접근한다.
  - hostPath는 팟이 삭제 되더라도 볼륨에 있던 데이터는 유지된다.
- nfs
- gcePersistentDisk, awsElasticBlockStore, azureFile, azureDisk
- cephfs, cinder, flexVolume, flocker, iscsi
- configMap, secret, downwardAPI
- persistentVolumeClaim
- csi
