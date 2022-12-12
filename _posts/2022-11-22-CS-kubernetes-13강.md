---
published: true
title: '[쿠버네티스] Chapter 9. ConfigMaps, Secret, Downward API'
layout: post
subtitle: 'csReview Kubernetes'
categories: csReview
tags: Kubernetes
comments: true
---

ConfigMap, Secret 및 Downward API를 사용하여 애플리케이션을 설정하는 것에 대해 알아보자.

### Command, Arguments, and ENV Variables
컨테이너 설정에는 다음 세 가지가 있다. 설정 변경마다 컨테이너 이미지를 재구성하지 않게 하드 코딩을 하지 않는다.
1. ENV
2. ENTRYPOINT - command
3. CMD - args
![commandArgs](https://sundongkim-dev.github.io/assets/img/kubernetes/commandArgs.png)

### Environment Variables
Env 필드는 환경변수와 그 값을 페어로 배열의 형태로 갖는다.
![env](https://sundongkim-dev.github.io/assets/img/kubernetes/env.png)

### ConfigMap
Pod manifest안의 configuration이 container image에 하드코딩하는 것보다 훨씬 낫지만 이상적인 상황은 아니다. Pod manifest에서 configuration을 분리하기 위해 configMap object를 만든다.

![configMap](https://sundongkim-dev.github.io/assets/img/kubernetes/configMap.png)

서로 다른 환경에 동일한 pod manifest를 배포할 수 있으며 동일한 configMap 이름을 사용하여 각 환경에 대해 서로 다른 configuration을 유지할 수 있다.

![configMap2](https://sundongkim-dev.github.io/assets/img/kubernetes/configMap2.png)

즉, pod이 생성될 때 이런 환경 변수나 설정값들을 변수로 관리해서 넣어주게 되어 pod을 배포할 때마다 다른 설정 정보를 반영하도록 할 수 있게 된다.

### configMap Volume

환경 변수는 작은 한 줄 값을 응용 프로그램에 전달하는 데 사용되며, 다중 줄 값은 일반적으로 파일로 전달된다. 즉, configMap volume을 사용하면 configuration을 파일 형태로 해서 pod에 공유하는 것이다.

### Secrets Object

- 인증 정보 및 암호화 키와 같은 중요한 보안 데이터를 유지하는 것이 목적이다. (Envoy 사이드카 컨테이너의 클라이언트를 인증하는 데 사용).
- configMap과 마찬가지로 암호에는 환경 변수와 파일을 컨테이너에 주입하는 데 사용할 수 있는 키-값 쌍이 포함되어 있다.

![secret](https://sundongkim-dev.github.io/assets/img/kubernetes/secret.png)

### Secret Volume

configMap 볼륨과 유사하지만, config map 대신 암호를 가리킨다. 마찬가지로 암호의 항목을 파일에 project하고 secret volume에 있는 파일들은 손상될 가능성이 적은 메모리 파일 시스템(tmpfs)에 저장된다.

![secretVolume](https://sundongkim-dev.github.io/assets/img/kubernetes/secretVolume.png)

### Downward API

configMap과 secrets를 사용하여 static configuration data를 애플리케이션에 전달할 수 있게 되었다.

하지만 사전에 알려지지 않은 데이터(팟 IP 및 이름, 클러스터 이름 등)는 어떻게 전달할까?  
Downward API!!!

- 환경변수 또는 파일을 통해 팟과 컨테이너의 메타데이터를 노출한다.
- 팟의 메타데이터, spec, status 필드의 값을 컨테이너에 주입한다.
- config map, secret과 유사하지만 값이 pod object에서 얻어진다는 점이 다르다.

![downwardAPI](https://sundongkim-dev.github.io/assets/img/kubernetes/downwardAPI.png)

- fieldRef: 팟의 일반 메타데이터
- resourceFieldRef: 컨테이너의 컴퓨팅 리소스 제약

### Summary

![projectedVolume](https://sundongkim-dev.github.io/assets/img/kubernetes/projectedVolume.png)
