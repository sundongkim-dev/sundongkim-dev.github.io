---
published: true
title: '[쿠버네티스] Chapter 5-A. Organizing API Objects Using Labels, Selectors, and Namespaces'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

### Labels
마이크로 서비스 아키텍처를 사용하면 배포된 마이크로 서비스의 수가 20개 이상을 쉽게 초과할 수 있기 때문에 임의적인 기준에 따라 그들을 더 작은 그룹으로 구성하는 방법이 필요하다. 이는 label을 통해 이루어진다.

레이블은 클러스터의 모든 사용자가 시스템에서 Object의 역할을 식별할 수 있도록 개체에 연결하는 키-값 쌍이다. 키와 값은 모두 원하는 대로 지정할 수 있는 간단한 문자열이다. 개체는 둘 이상의 레이블을 가질 수 있지만 레이블 키는 해당 object 내에서 고유해야 한다. 일반적으로 객체를 작성할 때 객체에 레이블을 추가하지만, 객체의 레이블은 나중에 변경할 수도 있다.

![labels](https://sundongkim-dev.github.io/assets/img/kubernetes/labels.png)

레이블은 레이블 선택기를 사용하여 리소스를 선택할 때 사용되며 선택기에 지정된 레이블을 기준으로 리소스를 필터링한다.
팟들은 stable, beta, canary, 총 3 가지 서비스를 운영하고 있다.

**라벨 선택기를 사용한 객체 필터링**  
이전 연습에서 포드에 추가한 레이블을 사용하면 각 개체를 식별하고 시스템에서 해당 개체를 찾을 수 있습니다. 지금까지 이러한 레이블은 개체를 나열할 때 추가 정보만 제공했다. 그러나 레이블 선택기를 사용하여 레이블을 기반으로 개체를 필터링할 때 레이블의 실제 성능이 발휘된다. 레이블 선택기를 사용하면 특정 레이블을 포함하는 포드 또는 기타 개체의 하위 집합을 선택하고 해당 개체에 대한 작업을 수행할 수 있다. 레이블 선택기는 개체가 특정 값을 가진 특정 레이블 키를 포함하는지 여부에 따라 개체를 필터링하는 기준이다.

예를 들면, nodeSelector: gpu: "true"라면, nodeSelector가 K8s에게 이 팟을 gpu=true 레이블을 갖고 있는 노드에게 배포하라라는 뜻이다.
