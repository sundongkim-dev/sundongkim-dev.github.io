---
published: true
title: '[프로그래머스] Level 1 - 문자열 다루기 기본'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 문자열 다루기 기본`](https://school.programmers.co.kr/learn/courses/30/lessons/12918)

---
## **문제 설명 및 풀이**

isdigit으로 숫자인지 쉽게 확인할 수 있다.

---
### C++스러운 나의 코드
```python
def solution(s):
    length = len(s)
    if length == 4 or length == 6:
        if s.isdigit():
            return True

    return False
```

### Pythonic한 풀이
```python
def solution(s):
    return s.isdigit() and len(s) in [4, 6]
```
