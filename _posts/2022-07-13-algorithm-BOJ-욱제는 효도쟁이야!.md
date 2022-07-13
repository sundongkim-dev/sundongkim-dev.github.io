---
published: true
title: '[백준] 14487번 - 욱제는 효도쟁이야!!'
layout: post
subtitle: 'BOJ 14487, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 14487번(브론즈 2) - 욱제는 효도쟁이야!!`](https://www.acmicpc.net/problem/14487)

---
## 문제 설명 및 풀이

제일 큰 값을 제외하고 돌면 된다.

---
### 나의 코드
```python
n = int(input())
li = list(map(int, input().split()))

print(sum(li) - max(li))
```
