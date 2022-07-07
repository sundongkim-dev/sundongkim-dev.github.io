---
published: true
title: '[프로그래머스] Level 1 - 음양 더하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 음양 더하기`](https://school.programmers.co.kr/learn/courses/30/lessons/76501)

---
## **문제 설명 및 풀이**

뭔가 마스킹을 통해 푸는 방법이 있을 것 같은데 나중에 찾아봐야겠다..

삼항 연산자와 sum을 사용하면 더 간단하게 풀 수 있다.

---
### C++스러운 나의 코드
```python
def solution(absolutes, signs):
    answer = 0
    for i,j in zip(absolutes, signs):
        if j:
            answer += i
        else:
            answer -= i
    return answer
```

### Pythonic한 풀이
```python
def solution(absolutes, signs):
    return sum(absolutes if sign else -absolutes for absolutes, sign in zip(absolutes, signs))
```
