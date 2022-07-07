---
published: true
title: '[프로그래머스] Level 1 - 내적'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 내적`](https://school.programmers.co.kr/learn/courses/30/lessons/70128)

---
## **문제 설명 및 풀이**

여전히 하나만 알고 둘은 모른다 ㅋㅋ...

왜 zip은 떠오르고 sum은 항상 안 떠오를까...

---
### 나의 코드
```python
def solution(a, b):
    answer = 0
    for i,j in zip(a,b):
        answer += i*j
    return answer
```

### Pythonic한 풀이
```python
def solution(a, b):
    return sum([x*y for x, y in zip(a,b)])
```
