---
published: true
title: '[프로그래머스] Level 1 - 소수 찾기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 소수 찾기`](https://school.programmers.co.kr/learn/courses/30/lessons/12921)

---
## **문제 설명 및 풀이**

소수 판별 문제도 문제 풀이에 자주 등장하는 녀석이다. 제곱근까지만 보면 소수인지 아닌지 확인할 수 있다.

하지만 메모리가 충분히 확보된 상황이라면 에라토스테네스의 체가 더 효과적이다. set으로 쉽게 구현할 수 있다.
---
### C++스러운 나의 코드
```python
def isPrime(n):
    if n == 1:
        return False
    for i in range(2, int(n**0.5)+1):
        if n%i == 0:
            return False
    return True

def solution(n):
    answer = 0
    for i in range(1, n+1):
        if isPrime(i):
            answer += 1
    return answer
```

### Pythonic한 풀이
```python
def solution(n):
    num = set(range(2, n+1))

    for i in range(2, n+1):
        if i in num:
            num -= set(range(2*i, n+1, i))
    return len(num)
```
