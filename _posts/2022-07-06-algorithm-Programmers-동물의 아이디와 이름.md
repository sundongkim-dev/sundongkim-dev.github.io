---
published: true
title: '[프로그래머스] Level 1 - 동물의 아이디와 이름'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 동물의 아이디와 이름`](https://school.programmers.co.kr/learn/courses/30/lessons/59403)

---
## **문제 설명 및 풀이**

SELET, FROM, ORDER BY(ASC, DESC)를 사용하는 아주 기초적인 문제이다.

문제의 나온 attribute들을 잘 보고 쿼리를 작성하면 된다. ~~따로 설명할 것이 없네,,~~

---
### MySQL 코드
```
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
ORDER BY ANIMAL_ID ASC
```
