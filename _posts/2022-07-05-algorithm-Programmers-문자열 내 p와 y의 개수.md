---
published: true
title: '[프로그래머스] Level 1 - 문자열 내 p와 y의 개수'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 문자열 내 p와 y의 개수`](https://school.programmers.co.kr/learn/courses/30/lessons/12916)

---
## **문제 설명 및 풀이**

count 함수를 통해 쉽게 구해줄 수 있다.

하지만 대소문자가 중요하지 않은 상황이라면 lower혹은 upper로 하나로 통일해주고 세어주는 방법 또한 있다.

---
### C++스러운 나의 코드
```python
def solution(s):

    p = s.count('p') + s.count('P')
    y = s.count('y') + s.count('Y')

    if p != y:
        return False
    return True
```

### 다른 풀이
```python
def solution(s):
    return s.lower().count('p') == s.lower().count('y')
```
