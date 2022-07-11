---
published: true
title: '[백준] 21313번 - 문어'
layout: post
subtitle: 'BOJ 21313, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 21313번(브론즈 2) - 문어`](https://www.acmicpc.net/problem/21313)

---
## 문제 설명 및 풀이

간단히 요약하면 문어의 수가 짝수이냐 홀수이냐로 나눠볼 수 있다.

짝수라면 1,2만으로 수열을 만들 수 있을테고,

홀수라면 양 옆의 서로 다른 문어와 손을 맞잡아야 하므로, 3이 나와야 하고 사전순이므로 마지막에 넣어주면 된다.

또한 리스트를 출력을 해줄 때, 일일이 for문으로 출력을 하는 것이 아니라 *를 사용하면 간단하게 한 줄로 출력해줄 수 있다.

---
### 나의 코드
```python
n = int(input())
ans = [1, 2] * (n//2) + ([3] if n%2 else [])
print(*ans)
```
