---
published: true
title: '[프로그래머스] Level 1 - 어린 동물 찾기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 어린 동물 찾기`](https://school.programmers.co.kr/learn/courses/30/lessons/59037)

---
## **문제 설명 및 풀이**

!=와 같은 의미로 쓰이는 <>를 알아야 풀 수 있는 문제이다. 결국 젊은 동물은 INTAKE_CONDITION attribute가 aged가 아닌 경우이다.

---
### MySQL 코드
```
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE INTAKE_CONDITION <> 'Aged'
ORDER BY ANIMAL_ID ASC
```
