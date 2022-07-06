---
published: true
title: '[프로그래머스] Level 1 - 약수의 합'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 약수의 합`](https://school.programmers.co.kr/learn/courses/30/lessons/12928)

---
## **문제 설명 및 풀이**

일일이 입력받은 수(n)만큼 돌아 약수인지 확인해주고 더해주었다. O(n)의 시간복잡도를 갖는다.

하지만 결국 약수는 n/2를 넘는 값은 자기 자신 밖에 없으므로 절반만 확인하면 된다는 것을 알 수 있다. 물론 시간복잡도로 따지면 똑같지만 연산횟수가 적다면 절반으로 줄인 것으로 차이가 크다.

---
### C++스러운 나의 코드
```python
def solution(n):
    answer = 0
    for i in range(1, n+1):
        if n%i == 0:
            answer += i
    return answer
```

### 다른 풀이
```python
def solution(num):
    return num + sum([i for i in range(1, (num // 2) + 1) if num % i == 0])
```
