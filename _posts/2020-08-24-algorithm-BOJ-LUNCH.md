---
published: true
layout: post
title: '[백준] 5543번 - 상근날드'
subtitle: 'BOJ 5543 from JOI 2012 Qualification #1'
categories: algorithm
tags: boj problems
comments: true
---
# 문제
> [`https://www.acmicpc.net/problem/5543`](https://www.acmicpc.net/problem/5543)

주어지는 세 종류의 버거 중의 제일 값싼 것, 그리고 두 종류의 음료중에서 보다 값싼 것의 금액을 구하는 것이 문제의 전부이다. 문제를 보자마자 삼항 연산자가 떠올랐고 버거끼리 비교를 해주어 최소값을 구하고, 음료도 마찬가지로 최소값을 구해주었다.

<script src="https://gist.github.com/sundongkim-dev/21f2a796a5160abdc391d5a6b05bf7bf.js"></script>

짜고보니 코드가 너무 지저분해서 한번 더 다듬었다. 우선, 쓸데없는 변수 선언이 많았고 둘째로는 필요없는 비교연산이었다.(3번만해도 되는데 4번이나 함.)
이와 별개로, 동일한 잦은 연산이라면 함수로 빼주는 습관을 들여야겠다.

<script src="https://gist.github.com/sundongkim-dev/38e9d97b091cafe3ec7b2cfb20d359c0.js"></script>
