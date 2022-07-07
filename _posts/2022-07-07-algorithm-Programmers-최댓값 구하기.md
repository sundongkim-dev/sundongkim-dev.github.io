---
published: true
title: '[프로그래머스] Level 1 - 최댓값 구하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 최댓값 구하기`](https://school.programmers.co.kr/learn/courses/30/lessons/59415)

---
## **문제 설명 및 풀이**

가장 최근에 들어온 동물은 언제 인지를 조회하는 문제이므로 DATETIME의 값이 클 것이다. ~~최근이니까~~

즉, max를 사용하면 바로 알 수 있다.

반대로 처음 들어온 동물이라면?? min을 사용하면 알 수 있다.

---
### MySQL 코드
```
SELECT max(DATETIME)
FROM ANIMAL_INS
```
