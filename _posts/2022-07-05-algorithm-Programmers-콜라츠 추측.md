---
published: true
title: '[프로그래머스] Level 1 - 콜라츠 추측'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 콜라츠 추측`](https://school.programmers.co.kr/learn/courses/30/lessons/12943)

---
## **문제 설명 및 풀이**

삼항 연산자를 활용하면 더욱 깔끔하게 풀 수 있다.

---
### 나의 코드
```python
def solution(num):
    answer = 0
    iters = 0
    while iters < 500:
        if num == 1:
            answer = iters
            break
        if num%2 == 0:
            num /= 2
        else:
            num = (num*3)+1
        iters += 1
    if num != 1:
        answer = -1
    return answer
```

### 삼항 연산자를 활용한 풀이
```python
def solution(num):
    for i in range(501):
        if num == 1:
            return i
        num = num/2 if num%2==0 else num*3+1
    return -1
```
