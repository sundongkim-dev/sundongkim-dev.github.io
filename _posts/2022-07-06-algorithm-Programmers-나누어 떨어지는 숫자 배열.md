---
published: true
title: '[프로그래머스] Level 1 - 나누어 떨어지는 숫자 배열'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 나누어 떨어지는 숫자 배열`](https://school.programmers.co.kr/learn/courses/30/lessons/12910)

---
## **문제 설명 및 풀이**

하나씩 나누어 떨어지는 지 확인해주고 정렬해주는 식으로 풀었다.

비어있는 리스트는 False라는 사실을 알게 되었다. 이를 통해 or로 만약 비어있다면 -1이 들어있는 배열을 return하는 방식으로 구할 수 있다. 빈 리스트가 거짓이므로 비어있다면 [-1]이 return 되는 것이다.

---
### C++스러운 나의 코드
```python
def solution(arr, divisor):
    answer = []
    for i in arr:
        if i%divisor == 0:
            answer.append(i)
    answer.sort()
    if len(answer) == 0:
        answer.append(-1)

    return answer
```

### Pythonic한 풀이
```python
def solution(arr, divisor):
    return sorted([n for n in arr if n%divisor == 0]) or [-1]
```
