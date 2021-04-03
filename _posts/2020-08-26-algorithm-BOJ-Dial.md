---
published: true
layout: post
title: '[백준] 5622번 - 다이얼'
subtitle: 'BOJ 5622, BAKA from COCI 2012/2013 Contest #6'
categories: algorithm
tags: boj problems
comments: true
---
# 문제
> [`https://www.acmicpc.net/problem/8958`](https://www.acmicpc.net/problem/8958)

각 알파벳에 해당하는 숫자를 다 더해서 출력해주면 되는 문제이다.  
처음에는 그냥 if문을 사용해 아스키코드로 ABC, DEF, GHI, JKL, MNO, PQRS, TUV, WXYZ를 나누어서 합을 구하였다.
<script src="https://gist.github.com/sundongkim-dev/96cbdfb0e136fbad169ac61eaacaf806.js"></script>

하지만 미리 알파벳들에 해당하는 값을 배열로 선언한 뒤에  
[문자형 데이터 - '0'](https://sundongkim-dev.github.io/algorithm/2020/08/25/algorithm-BOJ-NumOfNum/)을 사용하여 해당 배열에 접근하여 더해주면 매우 간단한 코드가 된다.
<script src="https://gist.github.com/sundongkim-dev/39d87e544d9c591c131de15f559217fd.js"></script>  
위의 코드는 다른 사람의 코드를 참고한 것인데, 역시 맞춘 문제일지라도 다른 사람의 코드를 보며 여러 사고를 익혀야 한다는 생각이 들었다. 단순히 답을 맞추기에 급급했던 것 같다.
