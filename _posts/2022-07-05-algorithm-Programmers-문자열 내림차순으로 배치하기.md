---
published: true
title: '[프로그래머스] Level 1 - 문자열 내림차순으로 배치하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 문자열 내림차순으로 배치하기`](https://school.programmers.co.kr/learn/courses/30/lessons/12917)

---
## **문제 설명 및 풀이**

sort에 reverse옵션을 true로 주면 리스트의 원소들을 내림차순으로 정렬할 수 있다.

---
### C++스러운 나의 코드
```python
def solution(s):
    answer = ''
    s = list(s)
    s.sort(reverse=True)
    for i in s:
        answer += i
    return answer
```

### Pythonic한 풀이
```python
def solution(s):
    return ''.join(sorted(s, reverse=True))
```
