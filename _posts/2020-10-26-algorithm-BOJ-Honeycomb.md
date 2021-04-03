---
published: true
layout: post
title: '[백준] 2292번 - 벌집'
subtitle: >-
  BOJ 2869, 벌집 from  ICPC, Asia Pacific, Korea > Seoul Nationalwide Internet
  Competition 2004 B번
categories: algorithm
tags: boj problems
comments: true
---
# 문제
> [`https://www.acmicpc.net/problem/2292`](https://www.acmicpc.net/problem/2292)

이 문제는 보자마자 육각형의 마지막 수들 간에 규칙이 있을것이라고 생각했다.
수들을 나열해보니 계차수열이었다. 계산해보면 1 + 6 * n * (n-1) / 2로 정리하면 3n^2 - 3n + 1이다.
나는 이를 함수로 바꿔 호출하는 형태로 풀었다.

다른 풀이들을 참고해보니 이런식으로 계차수열 자체를 반복문을 통해 더해주었다.
<script src="https://gist.github.com/sundongkim-dev/892f0e59543a506b3aaea20665ada75b.js"></script>

두 풀이중 어느 것이 나은지는 잘 모르겠으나, 메모리에 한해서는 후자가 훨씬 절약한것을 알 수 있다.
