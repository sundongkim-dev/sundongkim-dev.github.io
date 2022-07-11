---
published: true
title: '[백준] 22864번 - 피로도'
layout: post
subtitle: 'BOJ 22864, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# **문제**
> [`[백준] 22864번(브론즈 2) - 피로도`](https://www.acmicpc.net/problem/22864)

---
## **문제 설명 및 풀이**

피로도가 음수로 내려가지 않음을 유의하고 풀자.

---
### **나의 코드**
```python
A, B, C, M = map(int, input().split())

hour = 0
cur = 0
ans = 0

while hour < 24:
	if cur + A > M:
		cur -= C
		cur = max(cur, 0)
	else:
		cur += A
		ans += B
	hour += 1

print(ans)
```
