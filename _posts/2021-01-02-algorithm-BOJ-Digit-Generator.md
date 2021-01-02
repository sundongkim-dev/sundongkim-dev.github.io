---
published: true
layout: post
title: '[백준] 2231 - 분해합'
subtitle: >-
  BOJ 2231, Digit generator from ICPC > Regionals > Asia Pacific > Korea > Asia
  Regional - Seoul 2005 B번
categories: algorithm
tags: BOJ
comments: true
---
# **문제**
---
> [`https://www.acmicpc.net/problem/2231`](https://www.acmicpc.net/problem/2231)

## **문제 설명 및 풀이**
---
분해합은 생성자와 각 자릿수의 합을 의미하는데, 처음엔 그냥 1부터 시작해서 N까지 모든 경우의 수를 계산하여 제출했었다. 이래도 통과는 하지만 더 빠르게 구하는 방법이 있다.  
조금 생각해보면, 각 자릿수의 합이 생각보다 큰 값이 아니다. 예를 들어, 천의 자리를 생각해보자. 각 자릿수는 최대로 잡아봐야 9이므로, 9 * 4 = 36이다. 그렇다면 위 생성자는 결국 N-36보다 항상 크거나 같을 수 밖에 없게 된다. 이것을 확장해보면, 주어진 수의 자릿수를 구한 뒤 그 자릿수만큼 9를 곱해서 범위를 잡아 범위 안에 있는 수들만 살펴보면 되는 것이다.  
겉보기에는 브루트포스이지만, 커봐야 54개의 수만 살펴보면 금방 찾을 수 있는 것이다.  

## **코드**
---
<script src="https://gist.github.com/sundongkim-dev/1dfdf6762d8b25a48031ff5a1c4aaeb5.js"></script>
