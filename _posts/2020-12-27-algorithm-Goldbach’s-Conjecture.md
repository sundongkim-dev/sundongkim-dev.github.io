---
published: true
layout: post
subtitle: 'BOJ 9020, Goldbach’s Conjecture from ICPC, Asia Pacific, Korea Daejun 2011 E번'
categories: algorithm
tags: BOJ
comments: true
title: '[백준] 9020번 - 골드바흐의 추측'
---

# 문제
> [`https://www.acmicpc.net/problem/9020`](https://www.acmicpc.net/problem/9020)

골드바흐의 추측은 간단히 말해 2보다 큰 모든 짝수는 두 소수의 합으로 나타낼 수 있다는 것이다. 다만 문제에서는 다양한 답들 중, 두 소수의 제일 작은 답을 출력하라하였으므로, 주어진 수의 절반에서 시작해서 소수를 찾으면 되는 매우 쉬운 문제이다. 범위는 10,000까지이기에 에라토스테네스의 체를 이용하여 주어진 범위까지의 소수를 모두 찾은 후 연산하면 편하다.

<script src="https://gist.github.com/sundongkim-dev/61e2d5cfeacf2e948504f304970d3683.js"></script>
