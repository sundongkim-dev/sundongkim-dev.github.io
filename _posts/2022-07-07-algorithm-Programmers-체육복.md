---
published: true
title: '[프로그래머스] Level 1 - 체육복'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 체육복`](https://school.programmers.co.kr/learn/courses/30/lessons/42862)

---
## **문제 설명 및 풀이**

리스트를 만들어서 체육복을 갖고 있는 현황을 표현해주었다.

그리디하게 접근해서 빌려줄 수 있으면 먼저 빌려주는 형식으로 구현해주었다. 그렇게 체육복 소유 현황 리스트 p를 업데이트 해주며 구해주면 된다.

하지만 이렇게 풀면 분기가 너무 많아진다. 그냥 여분의 체육복을 갖고 있는 현황 리스트를 만들어서 앞선 사람을 우선적으로 주는 식으로 배분하면 된다. 이에 remove를 사용하면 효과적으로 제거할 수 있다.


---
### C++스러운 나의 코드
```python
def solution(n, lost, reserve):
    ans = 0
    p = [1 for i in range(1, n+1)]
    for l in lost:
        p[l-1] -= 1
    for r in reserve:
        p[r-1] += 1

    for idx, i in enumerate(p):
        if p[idx] > 1:
            if idx - 1 >= 0:
                if p[idx-1] < 1:
                    p[idx-1] += 1
                    p[idx] -= 1

            if idx + 1 < n:
                if p[idx+1] < 1:
                    if p[idx] > 1:
                        p[idx+1] += 1
                        p[idx] -= 1
    for i in p:
        if i>0:
            ans += 1
    return ans
```

### Pythonic한 풀이
```python
def solution(n, lost, reserve):
    reserve.sort()
    lost.sort()
    _reserve = [r for r in reserve if r not in lost]
    _lost = [l for l in lost if l not in reserve]

    for r in _reserve:
        f = r - 1
        b = r + 1
        if f in _lost:
            _lost.remove(f)
        elif b in _lost:
            _lost.remove(b)
    return n - len(_lost)
```
