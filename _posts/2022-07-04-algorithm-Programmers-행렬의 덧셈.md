---
published: true
title: '[프로그래머스] Level 1 - 행렬의 덧셈'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 행렬의 덧셈`](https://programmers.co.kr/learn/courses/30/lessons/12950)

---
## **문제 설명 및 풀이**

행렬 data는 numpy만 다뤄봐서 처음에 당황했다. 차근차근 print 찍어가면서 풀었다.  
두 행렬의 길이가 같아서 zip이라는 내장 함수로 쉽게 순회할 수 있었다.

여전히 for문을 사용할 때 내가 봐도 c++스러운 것이 느껴진다.  
하나의 리스트 안에서 처리하는 것을 체화해야 한다.

---
### C++스러운 나의 코드
```python
def solution(arr1, arr2):
    answer = []
    for i in zip(arr1, arr2):
        z = [x+y for x,y in zip(i[0],i[1])]
        answer.append(z)

    return answer
```

### Pythonic한 풀이
```python
def solution(A,B):
    answer = [[c + d for c, d in zip(a, b)] for a, b in zip(A,B)]
    return answer
```
