---
published: true
title: '[프로그래머스] Level 1 - 여러 기준으로 정렬하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 여러 기준으로 정렬하기`](https://school.programmers.co.kr/learn/courses/30/lessons/59404)

---
## **문제 설명 및 풀이**

ORDER BY 구문을 사용하여 정렬해주면 된다. 다만 정렬하고픈 여러 기준이 있다면, 우선적으로 적용하고 싶은 기준 순서대로 써주면 된다.

---
### MySQL 코드
```
SELECT ANIMAL_ID, NAME, DATETIME
FROM ANIMAL_INS
ORDER BY NAME ASC, DATETIME DESC
```
