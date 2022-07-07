---
published: true
title: '[프로그래머스] Level 1 - 로또의 최고 순위와 최저 순위'
layout: post
subtitle: 'Programmers, Level 1'
categories: algorithm
tags: programmers problems
comments: true
use_math: true
---

# **문제**

> [`[프로그래머스] level 1 - 로또의 최고 순위와 최저 순위`](https://school.programmers.co.kr/learn/courses/30/lessons/77484)

---
## **문제 설명 및 풀이**

lotto의 수가 당첨 넘버에 있는 지 확인하여 세주고 그렇지 않은 경우도 세주어서 최대와 최소를 인덱싱을 통해 구해주었다.

그러다 보니 코드가 많이 지저분하다.. 당첨 숫자가 나의 lottos에 얼마나 있는 지 확인하고 0만큼 더해주거나 말거나로 구하면 더 깔끔하게 구할 수 있다.

count라는 메소드로 0의 수는 쉽게 구해줄 수 있다.

혹은 당첨 번호를 대조하는 for문을 set의 집합연산으로 구해줄 수도 있다.

---
### C++스러운 나의 코드
```python
def solution(lottos, win_nums):
    answer = []
    same = 0
    diff = 0
    rank = [6,6,5,4,3,2,1]
    for i in lottos:
        if i == 0:
            continue
        if i in win_nums:
            same += 1
        else:
            diff += 1

    z = 6 - same - diff
    answer.append(rank[same+z])
    answer.append(rank[same])

    return answer
```

### 단순한 풀이
```python
def solution(lottos, win_nums):
    rank=[6,6,5,4,3,2,1]

    cnt_0 = lottos.count(0)
    ans = 0

    for x in win_nums:
        if x in lottos:
            ans += 1

    return rank[cnt_0 + ans],rank[ans]
```

```python
def solution(lottos, win_nums):
    rank = [6,6,5,4,3,2,1]
    return [rank[len(set(lottos) & set(win_nums)) + lottos.count(0)], rank[len(set(lottos) & set(win_nums))]]
```
