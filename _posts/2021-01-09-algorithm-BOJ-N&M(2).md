---
published: true
layout: post
title: '[백준] 15650번 - N과 M(2)'
subtitle: 'BOJ 15650, N & M(2)'
categories: algorithm
tags: BOJ
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/15649`](https://www.acmicpc.net/problem/15649)

## **문제 설명 및 풀이**
---
`백트래킹` 유형의 문제를 체화할 수 있는 연습문제이다. N과 M(1)과 크게 차이가 없다.  
[백트래킹과 N과 M (1) 풀이가 궁금하다면 클릭!!](https://sundongkim-dev.github.io/algorithm/2021/01/03/algorithm-BOJ-N&M/)  
N과 M (1)에선 `순열`을 구했다면, 이번 문제는 `조합`을 구하는 문제이다. BFS를 이용한 풀이로, 재귀 함수 호출에서 현재 택한 값의 이전값들은 고려하지 않게 for문의 i값을 함수에 넘겨 주면 된다. 즉, for문의 i값을 함께 재귀함수의 인자로 넘겨주면 이전의 찾은 조합은 다시 뽑지 않게 되는 것이다. 

## **코드**
---
<script src="https://gist.github.com/sundongkim-dev/47466087e72bcb4650f54625fb47da95.js"></script>
