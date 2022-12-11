---
published: true
title: '[쿠버네티스] Chapter 5-B. Advanced Scheduling'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

## Advanced Scheduling

### Taints and Tolerations
쿠버네티스 클러스터의 특정 노드에 테인트(Taint)를 설정할 수 있다. 기본적으로 테인트를 설정한 노드는 파드들을 스케줄링하지 않는다. 테인트를 설정한 노드에 파드들을 스케줄링하려면 파드에 톨러레이션(Toleration)을 설정해야 한다. 결국, 테인트는 톨러레이션에서 설정한 특정 파드들만 실행하고 다른 파드는 실행하지 못하게 한다. 목적은 노드 안의 특정 노드를 사용할 수 있는 팟을 제한하는데 사용된다.

![taints](https://sundongkim-dev.github.io/assets/img/kubernetes/taints.png)

### Effect Field
- NoSchedule: 톨러레이션 설정이 없으면 파드를 스케쥴링하지 않는다. (단, 기존 실행 팟은 적용 X)
- PreferNoSchedule: 톨러레이션 설정이 없으면 파드를 스케쥴링하지 않는다. 하지만 클러스터 내 자원이 부족하면 테인트를 설정한 노드에서도 파드를 스케쥴링할 수 있다.
- NoExecute: 톨러레이션 설정이 없으면 새로운 파드를 스케줄링하지 않으며, 기존 파드도 톨러레이션 설정이 없으면 종료시킨다.

Production(실제로 서비스 중인 version)과 non-production(개발 중인 서비스 version)을 분리할 Kubernetes 클러스터를 예로 들 수 있다.

### Node Affinity
노드는 팟의 대상이 되기 위해 노드 셀렉터로 해당 필드의 모든 레이블을 포함해야 했다. 좀 더 강력한 메카니즘인 node affinity가 등장했다.

노드 어피니티(Node Affinity)는 노드 셀렉터와 비슷하게 노드의 레이블을 기반으로 팟을 스케쥴링한다. 노드 어피니티와 노드셀렉터를 함께 설정할 수도 있으며, 이 때는 노드 어피니티와 노드셀렉터의 조건을 모두 만족하는 노드에 파드를 스케쥴링하게 된다.

`nodeSelector vs. nodeAffinity`
![nodeAffinity](https://sundongkim-dev.github.io/assets/img/kubernetes/nodeAffinity.png)

### Node Affinity Preference
- 배포 타겟: region > zone > hostname

![nodeAffinityPreference](https://sundongkim-dev.github.io/assets/img/kubernetes/nodeAffinityPreference.png)

노드 어피니티에는 두 가지 필드가 있다.
- requiredDuringSchedulingIgnoredDuringExecution : 스케쥴링하는 동안 꼭 필요한 조건
- preferredDuringSchedulingIgnoredDuringExecution : 스케쥴링하는 동안 만족하면 좋은 조건

파드가 이미 스케줄링되어 특정 노드에서 실행 중이라면 중간에 해당 노드의 조건이 변경되더라도 이미 실행 중인 팟은 그대로 실행된다.

### Inter-Pod Affinity
Node Affinity가 node의 label을 기준으로 팟이 배포될 node를 선택한다면, Inter-Pod Affinity 는 기존에 배포된 Pod를 기준으로 배포될 node를 결정합니다.

서비스 A의 파드와 서비스의 B의 파드가 자주 통신한다고 했을 때, Affinity는 이런 상황에서 서비스 A와 서비스 B의 파드들을 같은 노드에 속하게 만들어 효율을 높입니다. Backend 팟이 있는 노드에 frontend 팟을 배포하면 좋은 상황을 예로 들 수 있다.

내부적으로 pod affinity를 규칙들을 사용하여 점수를 매겨서 더 높은 점수를 갖는 노드에 할당한다.

### Co-locating pods
podAffinity의 topologyKey는 팟이 스케쥴링 될 대상 범위를 결정한다. topologyKey는 따로 정의할 수 있다.
- 동일한 geographical region 내
- 동일한 availability zone 내
- 동일한 host 내
- failure-domain.beta.kubernetes.io/**region**=europe-west1
- failure-domain.beta.kubernetes.io/**zone**=europe-west1-d
- kubernetes.io/**hostname**=gke-kubia-default-pool-dbb274c5a
![topologyKey](https://sundongkim-dev.github.io/assets/img/kubernetes/topologyKey.png)

### Pod Anti-Affinity
Inter-Pod Affinity 와는 반대로 특정 팟과 함께 배포되는 것을 피하도록 배포될 node를 결정하는 용도이다.

Anti-Affinity를 사용하면 CPU나 네트워크 같은 하드웨어 자원을 많이 사용하는 앱 컨테이너가 있을 때 여러 노드로 팟을 분산시킬 수 있다. 예를 들어 서비스를 운영하다가 트래픽이 많아졌다고 했을 때 Anti-Affinity가 설정되어 있지 않으면 팟 개수를 늘려도 이미 시스템 사용률이 높은 노드에 또 생성하여 퍼포먼스 문제가 있을 수 있다.
