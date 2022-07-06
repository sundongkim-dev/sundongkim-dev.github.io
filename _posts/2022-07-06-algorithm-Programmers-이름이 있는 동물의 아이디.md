---
published: true
title: '[프로그래머스] Level 1 - 이름이 있는 동물의 아이디'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 이름이 있는 동물의 아이디`](https://school.programmers.co.kr/learn/courses/30/lessons/59407)

---
## **문제 설명 및 풀이**

IS NOT NULL을 사용하여 해당 attribute가 채워진 record들을 가져올 수 있었다.

---
### MySQL 코드
```
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID ASC
```
