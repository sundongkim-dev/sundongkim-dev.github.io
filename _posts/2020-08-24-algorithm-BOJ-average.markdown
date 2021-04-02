---
layout: post
subtitle: 'BOJ 10039, average from JOI 2014 Qualification #1'
categories: algorithm
tags: BOJ 
comments: true
published: true
title: '[백준] 10039번 - 평균 점수'
---
# 문제
> [`https://www.acmicpc.net/problem/10039`](https://www.acmicpc.net/problem/10039)

점수가 **40점이 넘는지 아닌지만 판별**하면 되는 매우 쉬운 문제이다. 5명의 점수를 입력 받고, 40점이 넘으면 그대로, 40점이 안되면 40점으로 모두 더한 값을 전체 인원 수인 5명으로 나누면 끝난다. 주의할 점은, 문제에 제시되어 있듯이 평균점수는 항상 정수이므로 굳이 double이 아닌 int로 선언해주어도 된다. 이를 코드로 표현하면 아래와 같다.

<script src="https://gist.github.com/sundongkim-dev/23fd6b76e189779d0bab045fad6d6dab.js"></script>
