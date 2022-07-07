---
published: true
title: '[프로그래머스] Level 1 - 없는 숫자 더하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 없는 숫자 더하기`](https://school.programmers.co.kr/learn/courses/30/lessons/86051)

---
## **문제 설명 및 풀이**

set을 활용하면 쉽게 찾아낼 수 있다.

하지만 어차피 찾을 수 없는 수들의 합을 구하는 것이고, numbers의 모든 원소는 서로 다른 조건이 있기 때문에 총 합인 45에서 numbers의 합을 빼주면 쉽게 구할 수 있다.

---
### 나의 코드
```python
def solution(numbers):
    answer = -1
    s = set([1,2,3,4,5,6,7,8,9,0])

    s = s - set(numbers)
    answer = sum(s)

    return answer
```

### 간단한 풀이
```python
def solution(numbers):
    return 45 - sum(numbers)
```
