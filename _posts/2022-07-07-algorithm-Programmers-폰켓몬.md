---
published: true
title: '[프로그래머스] Level 1 - 폰켓몬'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 폰켓몬`](https://school.programmers.co.kr/learn/courses/30/lessons/1845)

---
## **문제 설명 및 풀이**

결국 n/2, 전체 종류의 수 중 최소를 취하면 되므로 min과 set을 사용하면 쉽게 풀 수 있다.

---
### 나의 코드
```python
def solution(nums):
    return min(len(nums)/2, len(set(nums)))
```
