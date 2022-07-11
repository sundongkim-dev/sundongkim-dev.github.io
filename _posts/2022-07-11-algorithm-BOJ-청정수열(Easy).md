---
published: true
title: '[백준] 25176번 - 청정수열(Easy)'
layout: post
subtitle: 'BOJ 25176, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 25176번(브론즈 1) - 청정수열(Easy)`](https://www.acmicpc.net/problem/19564)

---
## 문제 설명 및 풀이

맨 처음엔 바보 같이 생각했다.

~~어!? 조합 문제네!! 최근에 배운 itertools로 삭 구해서 혼쭐내야지!!~~

그냥 어떤 경우가 제일 최소 인지를 먼저 생각했어야 했다. 결국, 1122...NN의 수열이 제일 최솟값을 갖는 청정수열이므로 (11), (22), ..., (NN) 덩이들의 순서를 정해주면 되는 것으로, 답은 N!이다.

팩토리얼 재귀로 구현할까 했으나, math를 import하면 쉽게 구해줄 수 있다.

---
### 나의 코드
```python
import math
n = int(input())
print(math.factorial(n))
```
