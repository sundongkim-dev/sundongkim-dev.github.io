---
published: true
title: '[프로그래머스] Level 1 - 모의고사'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 모의고사`](https://school.programmers.co.kr/learn/courses/30/lessons/42840)

---
## **문제 설명 및 풀이**

for문을 돌며 일일이 구해주면 된다. 이 때 enumerate를 사용하면 index로 때 쉽게 카운트하고 답을 구할 수 있다.

---
### C++스러운 나의 코드
```python
def solution(answers):
    pattern1 = [1,2,3,4,5]
    pattern2 = [2,1,2,3,2,4,2,5]
    pattern3 = [3,3,1,1,2,2,4,4,5,5]
    score = [0, 0, 0]
    result = []

    for idx, answer in enumerate(answers):
        if answer == pattern1[idx%len(pattern1)]:
            score[0] += 1
        if answer == pattern2[idx%len(pattern2)]:
            score[1] += 1
        if answer == pattern3[idx%len(pattern3)]:
            score[2] += 1

    for idx, s in enumerate(score):
        if s == max(score):
            result.append(idx+1)

    return result
```

### Pythonic한 풀이
```python
def solution(arr):
    return (sum(arr) / len(arr))
```
