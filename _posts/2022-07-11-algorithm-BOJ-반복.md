---
published: true
title: '[백준] 19564번 - 반복'
layout: post
subtitle: 'BOJ 19564, 그리디'
categories: algorithm
tags: boj problems bronze
comments: true
---

# 문제
> [`[백준] 19564번(브론즈 1) - 반복`](https://www.acmicpc.net/problem/19564)

---
## 문제 설명 및 풀이

결국 이후의 글자가 이전의 글자 뒤에 나오는 글자라면 새로 입력할 필요가 없기 때문에, 이를 고려하여 계산해주면 된다.

---
### 나의 코드
```python
word = input()
print(sum([1 for x in range(1, len(word)) if word[x] <= word[x-1]]) + 1)
```
