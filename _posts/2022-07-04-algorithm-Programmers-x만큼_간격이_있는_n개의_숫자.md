---
published: true
title: '[프로그래머스] Level 1 - x만큼 간격이 있는 n개의 숫자'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - x만큼 간격이 있는 n개의 숫자, 2022 KAKAO BLIND RECRUITMENT`](https://programmers.co.kr/learn/courses/30/lessons/12954)

---
## **문제 설명 및 풀이**

매우 쉬운 문제였다. 하지만 앞으로 파이썬을 사용해서 풀기로 한 만큼 pythonic하게 풀어야겠다. 아무리 문제가 쉬워도 이런 방식의 풀이를 체화하기 위해 블로그에 남겨야겠다.


---
### C++스러운 나의 코드
```python
def solution(x, n):
    answer = []
    num = x
    for i in range(0, n):
        answer.append(x)
        x += num
    return answer
```

### Pythonic한 코드
```python
def solution(x, n):
    return [i * x + x for i in range(n)]
```
