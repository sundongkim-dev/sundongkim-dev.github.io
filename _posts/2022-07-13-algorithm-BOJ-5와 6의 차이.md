---
published: true
title: '[백준] 2864번 - 5와 6의 차이'
layout: post
subtitle: 'BOJ 2864, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 2864번(브론즈 2) - 5와 6의 차이`](https://www.acmicpc.net/problem/2864)

---
## 문제 설명 및 풀이

저번에 배운 replace를 활용해서 풀어주었다.

-1을 마지막 인자로 넣어주면, 문자열 안의 모든 target문자가 내가 지정한 문자로 바뀐다. 사기적이다..

나는 원본이 혹시나 바뀔까봐 tmp1에 먼저 a를 복사하고 하는 식으로 했는데 그냥 새로운 변수를 써주어도 된다는 것을 알았다.

---
### 나의 코드
```python
a, b = map(str, input().split())
tmp1, tmp2 = a, b # tmp1 = a.replace("6","5",-1) 이런식으로 해도 가능!!!
tmp3, tmp4 = a, b

MIN = int(tmp1.replace('6', '5', -1)) + int(tmp2.replace('6', '5', -1))
MAX = int(tmp3.replace('5','6',-1)) + int(tmp4.replace('5','6', -1))

print(MIN, MAX)
```
