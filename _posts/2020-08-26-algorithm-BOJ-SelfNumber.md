---
published: true
layout: post
title: '[백준] 4673번 - 셀프 넘버'
subtitle: 'BOJ 4673, Self Numbers from ICPC-Mid-Central Regional 1998 #D'
categories: algorithm
tags: BOJ
comments: true
---
# 문제
> [`https://www.acmicpc.net/problem/4673`](https://www.acmicpc.net/problem/4673)

셀프 넘버와 생성자에 대한 설명은 생략하겠다.   
처음 문제를 접근할 때에는 생성자가 있는지를 판별하기 위해 숫자 N이 입력값이라면 N이하의 모든 수를 체크해야 하나 싶었다.   
그러나, 조금 더 생각해보니 여사건으로 구해서 빼면 코드 짜기도 편하고 더 빠를 거라는 생각이 들었다. [양의 정수 자릿수 분할](https://sundongkim-dev.github.io/algorithm/2020/08/25/algorithm-BOJ-NumOfNum/)로 생성자를 구하였다. 구한 생성자는 인덱스 배열의 해당 값을 갖는 인덱스를 0으로 초기화해주었다. 결론적으로, 인덱스 배열에서 0이 아닌 값을 갖는다면, 그 수는 셀프 넘버이다. 
<script src="https://gist.github.com/sundongkim-dev/f32b0f0f7f9bb76610bfeb3f53344780.js"></script>
