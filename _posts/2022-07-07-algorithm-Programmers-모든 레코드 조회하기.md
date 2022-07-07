---
published: true
title: '[프로그래머스] Level 1 - 모든 레코드 조회하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 모든 레코드 조회하기`](https://school.programmers.co.kr/learn/courses/30/lessons/59034)

---
## **문제 설명 및 풀이**

가장 기본적인 문제이다. 모든 record를 보고 싶을 땐? *을 사용하면 된다.

---
### MySQL 코드
```
SELECT *
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```
