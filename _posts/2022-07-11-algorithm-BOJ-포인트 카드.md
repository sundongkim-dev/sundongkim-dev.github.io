---
published: true
title: '[백준] 14471번 - 포인트 카드'
layout: post
subtitle: 'BOJ 14471, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 14471번(브론즈 2) - 포인트 카드`](https://www.acmicpc.net/problem/14471)

---
## 문제 설명 및 풀이

당첨 도장이 찍힌 수가 많은 순서대로 정렬한 후 m-1개가 될 때까지 비용을 계산해주면 된다.

---
### 나의 코드
```python
n, m = map(int,input().split())
goal = m-1
cur = ans = 0
li = []

for i in range(m):
	tmp = list(map(int, input().split()))
	li.append(tmp)
li.sort(reverse=True)

for a,b in li:
	if cur == goal:
		break
	if a >= n:
		cur += 1
	else:
		ans += (n - a)
		cur += 1

print(ans)
```
