---
published: true
title: '[프로그래머스] Level 1 - 부족한 금액 계산하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 부족한 금액 계산하기`](https://school.programmers.co.kr/learn/courses/30/lessons/82612)

---
## **문제 설명 및 풀이**

레벨 1이라 후딱 풀고 다음 레벨 가야지 하는 마음에 자꾸 대충 풀게 된다.

이 문제 또한 저번의 [두 정수 사이의 합](https://sundongkim-dev.github.io/algorithm/2022/07/06/algorithm-Programmers-%EB%91%90-%EC%A0%95%EC%88%98-%EC%82%AC%EC%9D%B4%EC%9D%98-%ED%95%A9/)과 비슷하다.

이 역시, 가우스의 일화를 떠올려 볼 수 있다. 즉, 등차수열의 합으로 문제를 풀어낼 수 있다.

---
### C++스러운 나의 코드
```python
def solution(price, money, count):
    answer = -1
    num = 0
    idx = 1
    while count > 0:
        count -= 1
        num += price*idx
        idx += 1
    answer = max(num-money, 0)
    return answer
```

### Pythonic한 풀이
```python
def solution(price, money, count):
    return max(0,price*(count+1)*count//2-money)
```
