---
published: true
title: '[백준] 2720번 - 세탁소 사장 동혁'
layout: post
subtitle: 'BOJ 2720, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 2720번(브론즈 3) - 세탁소 사장 동혁`](https://www.acmicpc.net/problem/2720)

---
## 문제 설명 및 풀이

저번에 푼 동전 거스르는 문제와 동일하다.

저번에 배운대로 리스트를 이용해서 풀어주었다.

---
### 나의 코드
```python
t = int(input())

money = [25, 10, 5, 1]

for i in range(t):
    ans = []
    target = int(input())
    for j in money:
        ans.append(target//j)
        target %= j
    print(*ans)
```
