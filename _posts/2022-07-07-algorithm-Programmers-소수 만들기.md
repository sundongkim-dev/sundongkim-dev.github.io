---
published: true
title: '[프로그래머스] Level 1 - 소수 만들기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 소수 만들기`](https://school.programmers.co.kr/learn/courses/30/lessons/12977)

---
## **문제 설명 및 풀이**

서로 다른 3개를 고르기 위해 3중 for문을 사용하였고, itertools를 사용해서 조합을 구해주었다. 대충 구글링해서 사용하다 보니 바보같이 구현했던 것 같다.

애초부터 itertools의 combinations으로 서로 같은 값을 가진 다른 원소의 조합도 포함하여 구해줄 수 있더라...



---
### C++스러운 나의 코드
```python
import itertools

def isPrime(num):
    if num == 2 or num == 3:
        return True
    if num == 1:
        return False
    for i in range(2, int(num**0.5)+1):
        if num % i == 0:
            return False
    return True

def solution(nums):
    answer = 0
    s = []
    for idx1, i in enumerate(nums):
        for idx2, j in enumerate(nums):
            if idx1 >= idx2:
                continue
            for idx3, k in enumerate(nums):
                if idx2 >= idx3:
                    continue
                num = i+j+k
                s.append(num)
    for i in s:
        if isPrime(i):
            answer += 1

    p = itertools.combinations(nums, 3)
    for i in list(p):
        print(sum(i))

    return answer
```

### 깔끔한 풀이
```python
from itertools import combinations

def prime_number(x):
    answer = 0
    for i in range(1,int(x**0.5)+1):
        if x%i==0:
            answer+=1
    return 1 if answer==1 else 0

def solution(nums):
    return sum([prime_number(sum(c)) for c in combinations(nums,3)])
```
