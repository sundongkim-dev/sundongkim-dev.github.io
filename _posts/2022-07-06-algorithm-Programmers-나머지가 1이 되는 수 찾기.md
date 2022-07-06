---
published: true
title: '[프로그래머스] Level 1 - 나머지가 1이 되는 수 찾기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 나머지가 1이 되는 수 찾기`](https://school.programmers.co.kr/learn/courses/30/lessons/87389)

---
## **문제 설명 및 풀이**

처음부터 쭈욱 순회하면서 나머지가 1인 것을 찾아주면 된다.

조금 더 빨리 구하고 싶다면, 
---
### C++스러운 나의 코드
```python
def solution(n):
    for i in range(1, n):
        if n%i == 1:
            return i
```

### Pythonic한 풀이
```python
def solution(arr):
    return (sum(arr) / len(arr))
```
