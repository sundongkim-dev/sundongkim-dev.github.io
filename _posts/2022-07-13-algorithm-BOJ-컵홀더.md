---
published: true
title: '[백준] 2810번 - 컵홀더'
layout: post
subtitle: 'BOJ 2810, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 2810번(브론즈 1) - 컵홀더`](https://www.acmicpc.net/problem/2810)

---
## 문제 설명 및 풀이

좌석에 따른 컵홀더 수를 전부 구해주었다. 규칙을 잘 따라서 구현하면 된다. 이후 count로 컵홀더 수가 몇 개인지 구하고 사람과 최소값을 택해주었다.

푸는 내내 이렇게 밖에 못푸나 고민했었는데 역시나....

replace를 이렇게 사용하면 더 쉽게 구할 수 있다. 결국 입력으로 주어지는 좌석의 수가 곧 사람의 수이기 때문에 다 구해줄 필요가 없는 것이었다. ~~약간 벽 느낄 뻔 했다.~~

---
### 나의 코드
```python
num = int(input())
seats = list(input())
cups = ""
lcnt = 0
for idx, i in enumerate(seats):
    if i == 'S':
        cups += '*S'
    elif i == 'L':
        lcnt += 1
        # 이전에 S 또는 L 있음
        if idx-1 >= 0:
            # 바로 이전이 S
            if seats[idx-1] == 'S':
                cups += '*L'
                lcnt = 1
            # 바로 이전이 L
            elif seats[idx-1] == 'L':
                if lcnt > 2:
                    cups += '*L'
                    lcnt = 1
                else:
                    cups += 'L'
        # 처음 등장
        else:
            cups += '*L'
cups += '*'

print(min(cups.count('*'), num))
```

### 너무 간단한 코드
