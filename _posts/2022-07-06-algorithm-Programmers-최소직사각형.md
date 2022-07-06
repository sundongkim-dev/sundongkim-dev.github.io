---
published: true
title: '[프로그래머스] Level 1 - 최소직사각형'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 최소직사각형`](https://school.programmers.co.kr/learn/courses/30/lessons/86491)

---
## **문제 설명 및 풀이**

가로, 세로를 각각 큰 순서대로 정렬하고 가장 큰 값만을 취해서 만들어 주면 된다.

이를 더 pythonic하게 푼다면 아래와 같다. 어차피 큰 값들 중 제일 큰 값과 작은 값들 중 제일 작은 값을 구하면 되므로 굳이 나눠서 할 필요가 없다.

---
### C++스러운 나의 코드
```python
def solution(sizes):
    answer = 0
    w = 0
    h = 0
    for a,b in sizes:
        tmp = a
        if a < b:
            a = b
            b = tmp
        w = max(a, w)
        h = max(b, h)
    answer = w*h
    return answer
```

### Pythonic한 풀이
```python
def solution(sizes):
    return max(max(x) for x in sizes) * max(min(x) for x in sizes)
```
