---
published: true
title: '[백준] 10162번 - 전자레인지'
layout: post
subtitle: 'BOJ 10162, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 10162번(브론즈 4) - 전자레인지`](https://www.acmicpc.net/problem/10162)

---
## 문제 설명 및 풀이

리스트를 사용해서 인덱스로 접근하기, 리스트 한 번에 출력하기를 사용해보자!

---
### 나의 코드
```python
t = int(input())

a = [300, 60, 10]
ans = []

for i in a:
    ans.append(t // i)
    t %= i

if t > 0:
    print(-1)
else:
    print(*ans)
```
