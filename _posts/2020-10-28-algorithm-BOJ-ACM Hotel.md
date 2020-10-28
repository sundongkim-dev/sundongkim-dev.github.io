---
published: true
layout: post
title: '[백준]-10250번, ACM 호텔'
subtitle: >-
  BOJ 10250, ACM Hotel from ICPC Asia Pacific Korea > Daejeon Nationalwide
  Internet 2014 A번
categories: algorithm
tags: BOJ
comments: true
---
# 문제
> [`https://www.acmicpc.net/problem/10250`](https://www.acmicpc.net/problem/10250)

처음엔 그냥 반복문을 이용해서 일일이 순서를 셈했지만, > [`[백준]-2869번 달팽이는 올라가고 싶다`](https://sundongkim-dev.github.io/algorithm/2020/10/26/algorithm-BOJ-snail/) 이 문제를 해결하고 나니, 내 답도 달라졌다. 같은 원리로 층수와 호수를 구해줄 수 있었다. 딱 나눠지는 경우때문에 조건식을 쓰기 보다, 1을 빼주고 나중에 1을 더해줌으로써 더 간략하게 풀 수 있었다. 지금은 매번 이해하기 위해 잠시 생각해야하지만 아주 간단한 것임을 알고 이런 식을 잘 이용해야겠다.
<script src="https://gist.github.com/sundongkim-dev/f38b9b295837a8c8ae08a14d8fa65b70.js"></script>
