---
published: false
layout: post
subtitle: 'BOJ 2798, JACK from COCI 2011/2012 > Contest #6 1번'
categories: algorithm
tags: BOJ
comments: true
title: '[백준] 2798 - 블랙잭'
---
# **문제**
---
> [`https://www.acmicpc.net/problem/2798`](https://www.acmicpc.net/problem/2798)

## **문제 설명 및 풀이**
---
주어진 100개 이하의 카드에서 최대한 M에 가깝게 3장을 고르고 합을 출력하면 되는 문제이다. 브루트 포스라는 분류에 걸맞게, 모든 카드를 훑어보고 합을 계산해봐야 한다. 모든 카드 중 3개를 골라 합을 구하려면 3중 for문이 필요하다. 코드는 아래와 같다. 

## **코드**
---
<script src="https://gist.github.com/sundongkim-dev/d99d9c592132fd4b9fe151bc56b44960.js"></script>
