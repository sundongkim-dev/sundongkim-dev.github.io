---
published: true
title: '[프로그래머스] Level 1 - 핸드폰 번호 가리기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 핸드폰 번호 가리기`](https://programmers.co.kr/learn/courses/30/lessons/12948)

---
## **문제 설명 및 풀이**

이번에도 굉장히 c++스럽게 문제를 풀었다. 몇 번째 index부터 살리면 되는 지만 저장하고 for문으로 해결했다.  

파이썬은 문자열을 곱하기로 늘릴 수 있고, 음수 인덱스로 거꾸로 접근할 수 있음을 명심하자.

---
### C++스러운 나의 코드
```python
def solution(phone_number):
    answer = ''
    idx = len(phone_number)-4
    for i in range(0, idx):
        answer += '*'
    answer += phone_number[idx:]
    return answer
```

### Pythonic한 풀이
```python
def solution(s):
    return "*"*(len(s)-4) + s[-4:]
```
