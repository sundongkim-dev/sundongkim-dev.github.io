---
published: true
title: '[프로그래머스] Level 1 - 자릿수 더하기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 자릿수 더하기`](https://school.programmers.co.kr/learn/courses/30/lessons/12931)

---
## **문제 설명 및 풀이**

일일이 접근해서 풀 수 있지만, map이나 sum을 통해 더 간단하게 풀 수 있다.

map의 경우 자리별로 나누어 주기 위해 문자열로 한번 변환했다가 다시 int로 바꾸어주는 트릭을 사용할 수 있다.

---
### C++스러운 나의 코드
```python
def solution(n):
    answer = 0
    for i in str(n):
        answer += int(i)
    return answer
```

### Pythonic한 풀이
```python
def solution(number):
    return sum(map(int,str(number)))
```

```python
def solution(number):
  return sum([int(i) for i in str(number)])
```
