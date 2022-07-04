---
published: true
title: '[프로그래머스] Level 1 - 하샤드 수'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 하샤드 수`](https://programmers.co.kr/learn/courses/30/lessons/12947)

---
## **문제 설명 및 풀이**

입력을 문자열로 바꿔주어 한 글자씩 접근하고 int로 형변환해서 자릿수의 합을 구해주었다. 이후엔 문제대로 나누어 떨어지는 지 확인해주었다.

여전히 c++스럽다. 아래 보면 간단하게 리스트안에서 처리해준 것을 확인할 수 있다. 또한 sum 함수도 알게 되었다. ~~갈길이 멀다,,~~

---
### C++스러운 나의 코드
```python
def solution(x):
    answer = True
    num = 0
    for i in str(x):
        num += int(i)

    if x % num != 0:
        answer = False

    return answer
```

### Pythonic한 풀이
```python
def solution(n):
    return n % sum([int(c) for c in str(n)]) == 0
```
