---
published: true
title: '[프로그래머스] Level 1 - 최대공약수와 최소공배수'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 최대공약수와 최소공배수`](https://school.programmers.co.kr/learn/courses/30/lessons/12940)

---
## **문제 설명 및 풀이**

최대공약수와 최소공배수는 여러모로 코테에서 일부분으로 종종 출제되니 잘 알아두자. 재귀를 통해 간단하게 구현할 수 있다.

---
### 나의 코드
```python
def gcd(a, b):
    if a < b:
        return gcd(b,a)
    if a % b == 0:
        return b
    return gcd(b, a%b)

def lcm(a, b):
    num = gcd(a,b)
    return num*(a/num)*(b/num)

def solution(n, m):
    answer = []
    answer.append(gcd(n,m))
    answer.append(lcm(n,m))
    return answer
```
