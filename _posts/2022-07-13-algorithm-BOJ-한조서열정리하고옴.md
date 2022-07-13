---
published: true
title: '[백준] 14659번 - 한조서열정리하고옴ㅋㅋ'
layout: post
subtitle: 'BOJ 14659, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 14659번(브론즈 1) - 한조서열정리하고옴ㅋㅋ`](https://www.acmicpc.net/problem/14659)

---
## 문제 설명 및 풀이

최대 숫자를 계속 갱신하면서 더 높은 봉우리를 만나면 다시 0으로 초기화하고 구해주었다.

O(n)에 구할 수 있다.

---
### 나의 코드
```python
n = int(input())
li = list(map(int, input().split()))

ans = MAX = cnt = 0

for idx, i in enumerate(li):
    if MAX > i:
        cnt += 1
    else:
        MAX = i
        cnt = 0
    ans = max(ans, cnt)

print(ans)
```
