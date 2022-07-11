---
published: true
title: '[백준] 18238번 - ZOAC2'
layout: post
subtitle: 'BOJ 18238, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 22864번(브론즈 2) - ZOAC2`](https://www.acmicpc.net/problem/18238)

---
## 문제 설명 및 풀이

시계방향으로 세는 것이 가까운 지 반시계 방향으로 세는 것이 가까운 지를 세는 문제이다. 다만 아스키 코드 상으로 65부터 90에 위치하기 때문에 잘 처리해주어야 한다.

---
### 나의 코드
```python
string = input()
# A ~ Z = 65 ~ 90
pos = 65
ans = 0
for i in string:
	num = min(abs(ord(i)-pos), abs(min(pos, ord(i))+26 - max(pos, ord(i))))
	pos = ord(i)
	ans += num
print(ans)
```

### 간단한 코드
```python
s = "A"+input()
ans = 0
for i in range(len(s)-1):
    a = abs(ord(s[i])-ord(s[i+1]))
    ans += min(a,26-a)
print(ans)
```
