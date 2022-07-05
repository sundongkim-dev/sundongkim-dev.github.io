---
published: true
title: '[프로그래머스] Level 1 - 평균 구하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 평균 구하기`](https://school.programmers.co.kr/learn/courses/30/lessons/12944)

---
## **문제 설명 및 풀이**

sum과 len을 활용하여 풀면 쉽게 풀 수 있다.

---
### C++스러운 나의 코드
```python
def solution(arr):
    answer = 0
    for i in arr:
        answer += i
    answer /= len(arr)
    return answer
```

### Pythonic한 풀이
```python
def solution(arr):
    return (sum(arr) / len(arr))
```
