---
published: true
title: '[백준] 5585번 - 거스름돈'
layout: post
subtitle: 'BOJ 5585, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 5585번(브론즈 2) - 거스름돈`](https://www.acmicpc.net/problem/5585)

---
## 문제 설명 및 풀이

...내가 봐도 코드가 너무하다.

리스트를 사용해서 간단하게 풀자. Scalability도 챙기고!

---
### 나의 코드
```python
num = int(input())

target = 1000 - num
ans = 0

while target > 0:
    if target // 500:
        ans += target // 500
        target = target%500
    elif target // 100:
        ans += target // 100
        target = target%100
    elif target // 50:
        ans += target // 50
        target = target%50
    elif target // 10:
        ans += target // 10
        target = target%10
    elif target // 5:
        ans += target // 5
        target = target%5
    elif target // 1:
        ans += target // 1
        target = target%1

print(ans)
```
### 간단한 코드
```python
price = 1000 - int(input())
coin = [500, 100, 50, 10, 5, 1]
coinAmount = 0

for i in coin :
    coinAmount += price//i
    price = price%i

print(coinAmount)
```
