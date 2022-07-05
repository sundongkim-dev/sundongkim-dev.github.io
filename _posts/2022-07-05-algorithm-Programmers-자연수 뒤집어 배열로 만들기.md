---
published: true
title: '[프로그래머스] Level 1 - 자연수 뒤집어 배열로 만들기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 자연수 뒤집어 배열로 만들기`](https://school.programmers.co.kr/learn/courses/30/lessons/12932)

---
## **문제 설명 및 풀이**

일일이 insert하지 않고 map()과 list()를 활용하면 쉽게 풀 수 있다. 또한 list로 변환했기에 reversed로 정렬해주면 쉽게 뒤집을 수 있다.

**reversed**는 **원본을 변경하지 않고** iterator의 요소를 역순으로 리턴해준다.

반면, sort나 reverse는 원본을 변경하며 정렬한다.

---
### C++스러운 나의 코드
```python
def solution(n):
    answer = []
    for i in str(n):
        answer.insert(0,int(i))
    return answer
```

### Pythonic한 풀이
```python
def solution(n):
    return list(map(int, reversed(str(n))))
```
