---
published: true
title: '[프로그래머스] Level 1 - 수박수박수박수박수박수?'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 수박수박수박수박수박수?`](https://school.programmers.co.kr/learn/courses/30/lessons/12922)

---
## **문제 설명 및 풀이**

// 연산을 활용하여 몫을 바로 구해주면 쉽게 풀 수 있다.

파이썬은 문자열에 곱셈이 가능하므로 더 깔끔하게 풀 수 있다.
---
### 나의 코드
```python
def solution(n):
    answer = ''
    answer += '수박' * (n//2)
    if n%2 == 1:
        answer += '수'
    return answer
```

### Pythonic한 풀이
```python
def water_melon(n):
    s = "수박" * n
    return s[:n]
```
