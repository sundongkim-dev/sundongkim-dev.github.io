---
published: true
title: '[백준] 17224번 - APC는 왜 서브태스크 대회가 되었을까?'
layout: post
subtitle: 'BOJ 17224, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 17224번(브론즈 1) - APC는 왜 서브태스크 대회가 되었을까?`](https://www.acmicpc.net/problem/17224)

---
## 문제 설명 및 풀이

무슨 문제를 풀던 간에 한 개로 카운트 되기 때문에 어려운 것을 풀 수 있다면 먼저 풀어서 140점을 얻고, 그 후 쉬운 문제를 풀어서 100점을 추가하는 식으로 풀어야 한다. 그리디하게 말이다.

처음에 정렬해주고 어려운 것만 풀고 그러지 못한 문제들은 따로 리스트에 담아주어서 다시 한번 남은 카운트 수만큼의 문제를 풀때까지 순회를 했다.

더 간단한 풀이가 있어서 가져와보았다. 결국 각 문제 당 어려운 것을 풀 수 있으면 140으로 저장하고 그렇지 않고 쉬운 문제만 가능하다면 100을, 둘 다 못 푼다면 0으로 저장해주었다.

이후에 정렬하고 슬라이싱을 통해 쉽게 구해주었다.

---
### 나의 코드
```python
n, l, k = map(int, input().split())
li = [list(map(int, input().split())) for _ in range(n)]
li.sort()

newli = []
cnt = ans = 0
for a,b in li:
    if cnt >= k:
        break
    if l >= b:
        ans += 140
        cnt += 1
    else:
        newli.append([a,b])

for a,b in newli:
    if cnt >= k:
        break
    if l >= b:
        ans += 140
        cnt += 1
    elif l >= a:
        ans += 100
        cnt += 1

print(ans)
```

### 간단한 코드
```python
import sys
n, l, k = map(int, sys.stdin.readline().split())
p = list(map(lambda x: list(map(int, x.split())), sys.stdin.read().rstrip().split('\n')))
for i, x in enumerate(p):
	if l >= x[1]:
		p[i] = 140
	elif l < x[0]:
		p[i] = 0
	else:
		p[i] = 100
print(sum(sorted(p, reverse=True)[:k]))
```
