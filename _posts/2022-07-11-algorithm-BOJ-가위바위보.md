---
published: true
title: '[백준] 2930번 - 가위 바위 보'
layout: post
subtitle: 'BOJ 2930, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 2930번(브론즈 2) - 가위 바위 보`](https://www.acmicpc.net/problem/2930)

---
## 문제 설명 및 풀이

문제를 잘 읽는 것도 중요하다는 것을 또 한번 느끼게 된 문제이다...

상근이는 일대일 가위 바위 보를 절대 지지 않아서 세계 대회에 나가게 된 그런 스토리로 이해했는데 그게 아니라 진짜 1대1은 지지 않는 녀석이었다.

또한 개개인을 독립적으로 비교하기 때문에 각각의 경우를 모두 구해 최댓값을 취해주어야 한다.

구현 상에서 새로 배운 점 또한 있다.

친구들의 가위바위보 리스트를 입력받고 새로운 리스트에 append하면서 만들어 주었을텐데 input() for _ in range(n)으로 n만큼 문자열을 입력받아서 list로 만들어 줄 수 있었다.

또한, 딕셔너리 구조를 사용해서 R-S-P간의 관계를 쉽게 구해줄 수 있었다.

---
### 나의 코드
```python
num = int(input())
s = input()
friends = int(input())
fs = [input() for _ in range(friends)]

rsp = {'R':0,'S':1,'P':2}

honesty = 0
maxAns = 0

# 정직한 가위바위보
for i in range(num):
    ts = [[0, 'R'], [0, 'S'], [0, 'P']]
    for j in range(friends):
        if (rsp[s[i]] + 1) % 3 == rsp[fs[j][i]]:
            honesty += 2
        elif s[i] == fs[j][i]:
            honesty += 1
        # 모든 경우의 수
        for t in ts:
            if (rsp[t[1]] + 1) % 3 == rsp[fs[j][i]]:
                t[0] += 2
            elif t[1] == fs[j][i]:
                t[0] += 1
    maxAns += max(ts)[0]

print(honesty)
print(maxAns)

```
