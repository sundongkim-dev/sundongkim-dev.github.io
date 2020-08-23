---
layout: post
title: '[백준] 2844번-알람시계'
subtitle: 'BOJ 2844, SPAVANAC from COCI 2009/2010 > Contest #7 Q1'
categories: algorithm
tags: BOJ
comments: true
published: true
---

# 문제
> [`https://www.acmicpc.net/problem/2884`](https://www.acmicpc.net/problem/2884)

문제는 매우 간단하다. 45분 일찍 일어나기 위해 알람을 설정해야 하는 상황이다.  
처음에는 아래와 같이 긴 생각 없이 코딩을 했다.  
**45분보다 크다면** 45분을 빼도 시간에 지장이 없기에 그냥 뺀 값을 출력해주면 된다.  
만약, **45분보다 작다면** 시간에서 한시간, 즉 60분을 빌려와야 한다.  
그러나 여기서, 시간이 **0시라면 -1시가 아닌 23시**가 되어줘야 하기에 if문으로 예외처리를 할 수 있겠다. **0시가 아니라면** 그냥 시간에서 1을 빼주면 되겠다. 분은 60분을 빌려왔으므로 **(60분+m분-45분)**을 항상 만족한다.** 이를 코드로 표현하면 아래와 같다. 
<script src="https://gist.github.com/sundongkim-dev/51bcb8c3dc3d87d5fe729536852bb4ff.js"></script>

