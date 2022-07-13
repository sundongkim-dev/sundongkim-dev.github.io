---
published: true
title: '[백준] 11034번 - 캥거루 세마리2'
layout: post
subtitle: 'BOJ 11034, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 11034번(브론즈 3) - 캥거루 세마리2`](https://www.acmicpc.net/problem/11034)

---
## 문제 설명 및 풀이

종료 조건이 EOF인 문제를 처음 풀어 보았다. sys.stdin을 사용해서 풀수 있었다.

캥거루의 위치가 오름차순으로 주어져서 정렬할 필요도 없었다.

각 pair의 간격 -1 만큼이 캥거루가 최대 움직일 수 있는 횟수이다.

---
### 나의 코드
```python
import sys
for s in sys.stdin:
    a,b,c=map(int,s.split())
    print(max(c-b,b-a)-1)
```
