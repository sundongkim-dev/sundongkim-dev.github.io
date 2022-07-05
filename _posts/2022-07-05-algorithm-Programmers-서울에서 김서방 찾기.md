---
published: true
title: '[프로그래머스] Level 1 - 서울에서 김서방 찾기'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 서울에서 김서방 찾기`](https://school.programmers.co.kr/learn/courses/30/lessons/12919)

---
## **문제 설명 및 풀이**

리스트의 메소드인 index를 활용하면 쉽게 풀 수 있다. index는 넘겨진 item의 위치를 반환해주는 메소드이다.

직접적으로 +연산을 통해 더해주기 보단, format함수를 사용하는 것이 깔끔하다. 간단한건 앞선 방식이지만 앞으로 문자열을 다룰때에는 format을 자주 사용하자.

---
### 나의 코드
```python
def solution(seoul):
    return '김서방은 ' + str(seoul.index('Kim')) + '에 있다'
```

### 다른 풀이
```python
def findKim(seoul):
    return "김서방은 {}에 있다".format(seoul.index('Kim'))
```
