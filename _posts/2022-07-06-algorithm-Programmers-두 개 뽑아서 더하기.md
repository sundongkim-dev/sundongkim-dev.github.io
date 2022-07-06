---
published: true
title: '[프로그래머스] Level 1 - 두 개 뽑아서 더하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 두 개 뽑아서 더하기`](https://school.programmers.co.kr/learn/courses/30/lessons/68644)

---
## **문제 설명 및 풀이**

모든 경우의 수를 일단 리스트에 넣어놓고 unique한 item만 존재할 수 있는 set을 사용하여 풀어주었다.

---
### 나의 코드
```python
def solution(numbers):
    answer = []
    for idx1, i in enumerate(numbers):
        for idx2, j in enumerate(numbers):
            if idx1 == idx2:
                continue
            num = i+j
            answer.append(num)
    answer = list(set(answer))
    answer.sort()
    return answer
```
