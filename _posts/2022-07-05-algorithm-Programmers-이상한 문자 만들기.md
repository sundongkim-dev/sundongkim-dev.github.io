---
published: true
title: '[프로그래머스] Level 1 - 이상한 문자 만들기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 이상한 문자 만들기`](https://school.programmers.co.kr/learn/courses/30/lessons/12930)

---
## **문제 설명 및 풀이**

upper와 lower 함수로 힘들게 아스키 코드를 만지지 않고 쉽게 풀 수 있다.

---
### 나의 코드
```python
def solution(s):
    answer = ''
    idx = 0
    for l in s:
        if l == ' ':
            answer += ' '
            idx = 0
        else:
            if idx%2 == 0:
                answer += l.upper()
            else:
                answer += l.lower()
            idx += 1
    return answer
```
