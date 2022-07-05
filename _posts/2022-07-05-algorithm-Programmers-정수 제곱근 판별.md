---
published: true
title: '[프로그래머스] Level 1 - 정수 제곱근 판별'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 정수 제곱근 판별`](https://school.programmers.co.kr/learn/courses/30/lessons/12934)

---
## **문제 설명 및 풀이**

python은 나누기 연산을 하면 정수형이 아니라 실수형을 갖는다. 이를 활용하여 int형변환을 취해주었을때 값이 같다면 제곱근임을 알 수 있다.

혹은 1로 나누어 떨어진다면 이 또한 제곱근이라고 판별해줄 수 있다.

---
### 나의 코드
```python
def solution(n):
    answer = 0
    num = n**(1/2)
    if num == int(num):
        answer = (num+1)**2
    else:
        answer = -1
    return answer
```

### 다른 풀이
```python
def solution(n):
    sqrt = n ** (1/2)

    if sqrt % 1 == 0:
        return (sqrt + 1) ** 2
    return -1
```
