---
published: true
title: '[프로그래머스] Level 1 - 이름이 없는 동물의 아이디'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 이름이 없는 동물의 아이디`](https://school.programmers.co.kr/learn/courses/30/lessons/59039)

---
## **문제 설명 및 풀이**

해당 attribute가 비어 있다면 IS NULL로 확인할 수 있다.

---
### MySQL 코드
```
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NULL
ORDER BY ANIMAL_ID ASC
```
