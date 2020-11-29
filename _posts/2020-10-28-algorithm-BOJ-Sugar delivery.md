---
published: true
layout: post
subtitle: 'BOJ 2839, ŠEĆER from  COCI 2010/2011 > Contest #7 1번'
categories: algorithm
tags: BOJ
comments: true
title: '[백준]-2839번, 설탕 배달'
---
# 문제
> [`https://www.acmicpc.net/problem/2839`](https://www.acmicpc.net/problem/2839)

적은 봉지 수를 가져가기 위해서는 최대한 5kg을 많이 쓰면 된다.  
이를 위해선 반복문 안에서 조건식의 순서가 중요하다.   
5로 나누어지는지 우선 확인하고, 그렇지 않으면 3으로 나눠지는지 확인해야 한다.  
그 다음은 5와 3으로도 나누어지지 않을 경우를 걸러내기 위해 5보다 크다면 5를 뺴주고  
음수가 되도록 유도하면 된다.  
처음에는 조건문을 어떻게 해야 헷갈릴 수 있지만 무엇이 우선되어야 하는가를 생각하면 간단하다.  

<script src="https://gist.github.com/sundongkim-dev/65736d9149963982c05ceb294fe2856b"></script>

