---
published: true
title: '[프로그래머스] Level 1 - 같은 숫자는 싫어'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 같은 숫자는 싫어`](https://school.programmers.co.kr/learn/courses/30/lessons/12906)

---
## **문제 설명 및 풀이**

연속적이면 제거하는 것이므로 첫 번째 인덱스를 제외하고 계속 이전 인덱스의 값과 비교해주면 된다.

[-1:]과 같은 접근이 빈 배열에서는 작동하지 않을 줄 알았는데 작동하더라,, 이를 통해 더 깔끔하게 구현할 수 있다.

---
### C++스러운 나의 코드
```python
def solution(arr):
    tmp = []
    for idx, i in enumerate(arr):
        if idx == 0:
            tmp.append(i)  
            continue
        if i == arr[idx-1]:
            continue
        else:
            tmp.append(i)
    return tmp
```

### Pythonic한 풀이
```python
def solution(s):
    a = []
    for i in s:
        if a[-1:] == [i]:
            continue
        a.append(i)
    return a
```
