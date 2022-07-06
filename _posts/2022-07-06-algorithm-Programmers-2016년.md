---
published: true
title: '[프로그래머스] Level 1 - 2016년'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 2016년`](https://school.programmers.co.kr/learn/courses/30/lessons/12901)

---
## **문제 설명 및 풀이**

윤년임을 먼저 알려주었기 때문에 2월은 29일까지 있다. 그냥 리스트에 다 담아주어서 인덱스로 접근해서 답을 구했다.

이를 조금 더 다듬는 다면 아래와 같이 리스트 안에서 인덱싱과 sum을 통해 구해 줄 수 있다.

---
### C++스러운 나의 코드
```python
def solution(a, b):
    answer = ''
    d = [31,29,31,30,31,30,31,31,30,31,30,31]
    day = ['FRI', 'SAT', 'SUN', 'MON', 'TUE', 'WED', 'THU']

    n = 0
    for i in range(1, a):
        n += d[i-1]
    n += b
    n = n%7
    answer = day[n-1]
    return answer
```

### 깔끔한 풀이
```python
def solution(a,b):
    months = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
    days = ['FRI', 'SAT', 'SUN', 'MON', 'TUE', 'WED', 'THU']
    return days[(sum(months[:a-1])+b-1)%7]
```
