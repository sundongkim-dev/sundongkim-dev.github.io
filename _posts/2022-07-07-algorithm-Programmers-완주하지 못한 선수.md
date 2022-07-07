---
published: true
title: '[프로그래머스] Level 1 - 완주하지 못한 선수'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 완주하지 못한 선수`](https://school.programmers.co.kr/learn/courses/30/lessons/42576)

---
## **문제 설명 및 풀이**

Collections라는 모듈을 처음 알게 되었다. 뭐가 되었든 수를 세어주는 데 강력한 기능들을 갖고 있다. 리스트 안의 요소들을 요소 별로 몇 개 있는 지 딕셔너리로 나타내 주기도 하고, 최빈값을 쉽게 구해주기도 한다.

또한 문제처럼 산술/집합 연산 또한 가능하다!! 그래서 쉽게 마치 집합처럼 쉽게 구할 수 있었다. list로 형변환 또한 가능하다.

---
### Counter를 이용한 코드
```python
from collections import Counter
def solution(participant, completion):

    return list(Counter(participant) - Counter(completion))[0]
```
