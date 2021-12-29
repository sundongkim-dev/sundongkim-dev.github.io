---
published: false
title: '[컴퓨터 보안] Intrusion Detection'
layout: post
subtitle: 'csReview Computer Security'
categories: csReview
tags: ComputerSecurity
comments: true
---

# Intrusion Detection
보안에 대해 가장 널리 알려진 두 가지 위협은 malware와 intruder(침입자)이다. Intruder는 일반적으로 해커 혹은 크래커라고도 하는데 이번 장에서는 이러한 intruder를 탐지하는 것에 대해 알아볼 예정이다.
Intruder는 아래와 같이 총 3 가지의 class로 나눠볼 수 있다.
1. masquerader(가면)
시스템에 침투하여 합법적인 사용자 계정을 이용하는 허가되지 않은 개인을 말한다.(outsider)
2. misfeasor(실수)
권한을 잘못 사용하는 합법적인 사용자를 말한다.(insider)
3. clandestine user(비밀 사용)
insider일수도 있고, outsider일 수도 있는 존재로
