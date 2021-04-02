---
layout: post
title: '[백준] 2844번 - 알람시계'
subtitle: 'BOJ 2844, SPAVANAC from COCI 2009/2010 > Contest #7 Q1'
categories: algorithm
tags: boj problems
comments: true
published: true
---

# 문제
> [`https://www.acmicpc.net/problem/2884`](https://www.acmicpc.net/problem/2884)

문제는 매우 간단하다.  
45분 일찍 일어나기 위해 알람을 설정해야 하는 상황이다.  
처음에는 아래와 같이 코딩을 했다.  
**45분보다 크다면** 45분을 빼도 시간에 지장이 없기에 그냥 뺀 값을 출력해주면 된다.  
만약, **45분보다 작다면** 시간에서 한시간, 즉 60분을 빌려와야 한다.  
그러나 여기서, 시간이 **0시라면 -1시가 아닌 23시**가 되어줘야 하기에 if문으로 예외처리를 할 수 있겠다. **0시가 아니라면** 그냥 시간에서 1을 빼주면 되겠다. 분은 60분을 빌려왔으므로 **(60분+m분-45분)**을 항상 만족한다.** 이를 코드로 표현하면 아래와 같다.  

<script src="https://gist.github.com/sundongkim-dev/51bcb8c3dc3d87d5fe729536852bb4ff.js"></script>

조금 다른 관점으로 생각해보면, 분의 경우 -45분이나 +15분은 동일한 결과를 낸다는 것을 알 수 있다. 그렇기 때문에 60+m-45를 **(m+15)%60**으로도 표현하면 굳이 if문을 쓰지 않아도 된다. 이를 시간에 적용해보면, **(h+23+(m+15)/60)%24**이 되며, 이 경우 또한 굳이 if문을 쓰지 않아도 된다. 내용을 코드에 반영해보면, 아래와 같다.

<script src="https://gist.github.com/sundongkim-dev/a2a7c784acfb9d8ec04a109d8cbbdd58.js"></script>

이 문제를 기점으로, 이미 풀고 맞은 문제여도 다시 돌아보며 다른 방법은 무엇이 있는지 더 생각해봐야겠다.
