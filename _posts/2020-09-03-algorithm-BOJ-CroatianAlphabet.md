---
published: true
layout: post
title: '[백준] 2941번 - 크로아티아 알파벳'
subtitle: 'BOJ 4673, Self Numbers from ICPC-Mid-Central Regional 1998 #D'
categories: algorithm
tags: BOJ
comments: true
---
# 문제
> [`https://www.acmicpc.net/problem/2941`](https://www.acmicpc.net/problem/2941)

처음엔 문제 그대로 표에 따라 if-else문을 작성해서 문제를 풀어주었다. 
<script src="https://gist.github.com/sundongkim-dev/1fa8f6e488f429a32af01d34a6ed1077.js"></script>

하지만, -와 =가 아니라면 무조건 하나의 알파벳이기 때문에 이를 기준으로 if-else문을 다시 짰더니 훨씬 코드가 간결해졌다.
<script src="https://gist.github.com/sundongkim-dev/0e31b50fcd444637f7ff67fbcab327b9.js"></script>
