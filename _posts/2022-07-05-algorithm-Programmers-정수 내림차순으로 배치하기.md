---
published: true
title: '[프로그래머스] Level 1 - 정수 내림차순으로 배치하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 정수 내림차순으로 배치하기`](https://school.programmers.co.kr/learn/courses/30/lessons/12933)

---
## **문제 설명 및 풀이**

list()를 활용하면 간단히 리스트로 변환해준다. ~~일일이 append를 하는 나란 바보,,~~ 정렬한 이후 이를 문자열로 바꾸는 것도 join을 활용하면 간단하다.

---
### C++스러운 나의 코드
```python
def solution(n):
    answer = ""
    li = []
    for i in str(n):
        li.append(i)
    li.sort(reverse=True)
    for i in li:
        answer += i
    answer = int(answer)
    return answer
```

### Pythonic한 풀이
```python
def solution(n):
    li = list(str(n))
    li.sort(reverse = True)
    return int("".join(li))
```
