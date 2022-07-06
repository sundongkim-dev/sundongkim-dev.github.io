---
published: true
title: '[프로그래머스] Level 1 - 예산'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 예산`](https://school.programmers.co.kr/learn/courses/30/lessons/12982)

---
## **문제 설명 및 풀이**

최대한 많이 지원해야하므로 이는 그리디로 해결할 수 있다. 즉, 정렬하고 하나씩 빼고 카운트를 늘려주면 된다.

---
### 나의 코드
```python
def solution(d, budget):
    answer = 0
    d.sort()
    for i in d:
        if budget - i >= 0:
            budget -= i
            answer += 1
        else:
            break
    return answer
```
