---
published: true
layout: post
subtitle: 'BOJ 4948, Chebyshevs Theorem from ICPC, Asia Pacific, Japan 2011> Contest A번'
categories: algorithm
tags: boj problems
comments: true
title: '[백준] 4948번 - 베르트랑 공준'
---
# 문제
> [`https://www.acmicpc.net/problem/4948`](https://www.acmicpc.net/problem/4948)

앞서 게재한 소수 구하기에서 에라토스테네스의 체를 사용해보기 좋은 문제이다. 범위가 123456의 두배 범위안의 소수를 모두 알아야하는 문제기 때문이다. 복습하기 좋은 문제이므로, 에라토스테네스의 체를 이용해 코딩해보자!

<script src="https://gist.github.com/sundongkim-dev/d9b1346fa8712074ebbb2ed1408c082f.js"></script>

그저 참고용인데, 그냥 소수판별해서 개수를 센 것과 에라토스테네스의 체를 사용한 알고리즘의 실행시간 비교이다. 백준의 채점 결과를 가져온 것이라 실제 실행시간과 내 코드에 최적화 변수가 있겠지만 그래도 차이가 제법 나는 것을 알 수 있다.

<img src="https://sundongkim-dev.github.io/assets/img/Execution_Prime.png" width="547" height="139">
