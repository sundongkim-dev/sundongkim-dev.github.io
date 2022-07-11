---
published: true
title: '[백준] 14665번 - 욱제는 도박쟁이야!!'
layout: post
subtitle: 'BOJ 15881, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 14655번(브론즈 1) - 욱제는 도박쟁이야!!`](https://www.acmicpc.net/problem/14665)

---
## 문제 설명 및 풀이

문제 설명을 정말 뭐같이 해놨는데,,,

결국 배열의 인덱스 상관없이 계속 연속해서 뒤집을 수 있다는 것이다. 즉, 동전이 5개라면 (1,2,3), (2,3,4), (3,4,5), (4,5), (5) 이런식으로 다 뒤집을 수 있다는 이야기다.

~~결국 곱하기 2하면 되는데 왜 다 더해주었을까,,~~

---
### 나의 코드
```python
n = int(input())
li1 = list(map(int, input().split()))
li2 = list(map(int, input().split()))

ans = 0
for i in li1:
	ans += abs(i)
for i in li2:
	ans += abs(i)
print(ans)

```

### 간단한 코드
```python
input()
a=map(lambda x: abs(int(x)), input().split())
print(sum(a)*2)
```
