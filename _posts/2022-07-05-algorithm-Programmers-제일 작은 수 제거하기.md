---
published: true
title: '[프로그래머스] Level 1 - 제일 작은 수 제거하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 제일 작은 수 제거하기`](https://school.programmers.co.kr/learn/courses/30/lessons/12935)

---
## **문제 설명 및 풀이**

중복되는 원소가 없으므로 min을 활용하여 풀어줄 수 있다. 길이가 1이라면 그냥 -1을 담아서 리턴해주면 된다.

---
### C++스러운 나의 코드
```python
def solution(arr):
    answer = arr
    min = arr[0]
    if len(arr) == 1:
        answer.append(-1)
    else:
        for i in arr:
            if min > i:
                min = i

    answer.remove(min)
    return answer
```

### min 활용한 풀이
```python
def solution(arr):
    answer = []
    if len(arr) == 1:
        answer.append(-1)
    else:
        answer = arr
        answer.remove(min(answer))
    return answer
```
