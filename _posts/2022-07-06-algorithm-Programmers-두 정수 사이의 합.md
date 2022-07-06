---
published: true
title: '[프로그래머스] Level 1 - 두 정수 사이의 합'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 두 정수 사이의 합`](https://school.programmers.co.kr/learn/courses/30/lessons/12912)

---
## **문제 설명 및 풀이**

입력되는 두 수의 대소관계가 랜덤하기 때문에 구하기 쉽게 함수를 통해 대소관계를 일정하게 하고 리스트로 구해주었다.

점점 c++스러운 코드에서 pythonic하게 풀어가는 것 같다.

하지만 수학적으로 풀 수도 있다. 결국 구간 내의 원소의 합을 구하는 것이므로 가우스의 일화를 떠올려 볼 수 있다. [a,b]의 합은 $x+y=1$ 이다. 이를 코드로 표현하면 아래와 같다.

---
### 나의 코드
```python
def getSum(a,b):
    if a>b:
        return getSum(b,a)
    else:
        p = [n for n in range(a,b+1)]
        return sum(p)

def solution(a, b):  
    return getSum(a,b)
```

### 다른 풀이
```python
def solution(a, b):
    return (abs(a-b)+1)*(a+b)//2
```
