---
published: true
title: '[프로그래머스] Level 1 - 3진법 뒤집기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 3진법 뒤집기`](https://school.programmers.co.kr/learn/courses/30/lessons/68935)

---
## **문제 설명 및 풀이**

[::-1]로 string을 뒤집을 수 있다는 것을 알게 되었다.

나는 문제 그대로 노가다(?)성으로 진법을 바꿨는데, int형변환에 알고보니 n진법으로 만들 수 있는 기능이 있었다.

두 가지나 배울 수 있는 문제이다.

---
### 나의 코드
```python
def solution(n):
    answer = 0

    tmp = ""
    while int(n) > 0:
        tmp += str(int(n)%3)
        n /= 3

    tmp = tmp[::-1]
    start = 1
    for i in tmp:
        answer += int(i)*start
        start *= 3
    return answer
```

### 간단한 풀이
```python
def solution(n):
    tmp = ''
    while n:
        tmp += str(n % 3)
        n = n // 3

    answer = int(tmp, 3)
    return answer
```
