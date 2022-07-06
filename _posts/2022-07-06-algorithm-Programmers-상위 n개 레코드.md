---
published: true
title: '[프로그래머스] Level 1 - 상위 n개 레코드'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 상위 n개 레코드`](https://school.programmers.co.kr/learn/courses/30/lessons/59405)

---
## **문제 설명 및 풀이**

이왕 python으로 언어를 바꾸는 김에 sql문제들도 풀어보자. 필자는 수업 시간에 MySQL로 배워서 이를 언어로 선택하였다.

이 문제는 LIMIT 구문을 알면 쉽게 풀 수 있다. 상위 n개를 뽑아 낼 수 있는 구문이다.

---
### MySQL 코드
```
SELECT NAME
FROM ANIMAL_INS
ORDER BY DATETIME ASC LIMIT 1
```
