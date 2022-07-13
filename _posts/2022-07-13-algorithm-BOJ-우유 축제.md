---
published: true
title: '[백준] 14720번 - 우유 축제'
layout: post
subtitle: 'BOJ 14720, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 14720번(브론즈 3) - 우유 축제`](https://www.acmicpc.net/problem/14720)

---
## 문제 설명 및 풀이

규칙에 맞는 우유를 파는 가게라면 무조건 +1 해주면 끝이다.

---
### 나의 코드
```python
n = int(input())

li = list(map(int, input().split()))

ans = target = 0

for i in li:
    if i == target:
        ans += 1
        target = (target + 1)%3

print(ans)
```
