---
published: true
title: '[백준] 15881번 - Pen Pineapple Apple Pen'
layout: post
subtitle: 'BOJ 15881, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 15881번(브론즈 1) - Pen Pineapple Apple Pen`](https://www.acmicpc.net/problem/15881)

---
## 문제 설명 및 풀이

count를 써주면 그냥 간단하게 구할 수 있다니...뭔가 겹쳐서 구할 것 같았는데 아니었다..

count는 셀 때 해당 문자열을 찾았다면 그 다음 인덱스부터 또 세어 주는 것을 명심하자!!

---
### 나의 코드
```python
n = int(input())
li = list(input())

ans = 0
idx = 0
while True:
	if idx >= n-3:
		break
	if li[idx] == 'p' and li[idx+1] == 'P' and li[idx+2] == 'A' and li[idx+3] == 'p':
		ans += 1
		idx += 4
	else:
		idx += 1

print(ans)
```

### 간단한 코드
```python
input()
print(input().count('pPAp'))
```
